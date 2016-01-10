= HELPER-PROTOCOL =

[uim:doc/HELPER-PROTOCOL](http://uim.googlecode.com/svn/trunk/doc/HELPER-PROTOCOL)より転載



To communicate between uim-related processes such as GUI applications and toolbar applets, uim uses the helper system. This file describes the helper protocol within uim.

## Network topology and message passing ##

The message based helper protocol participants form a peer-to-peer star topology network connected via central uim-helper-server using UNIX domain socket.

```
               +-----------------+ ----- uim-toolbar-gtk
uim app1 ----- |uim-helper-server| ----- uim app2
uim app3 ----- +-----------------+ ----- uim configuration tool
```

Although uim-helper-server is named as 'server', it only means 'listen to the connections'. The server is currently implemented as simple message reflector, so the network always behaves as broadcasting.

```
          msg  +-----------------+ ----> uim-toolbar-gtk
uim app1 ----> |uim-helper-server| ----> uim app2
uim app3 <---- +-----------------+ ----> uim configuration tool
```

All participants receives the message from uim app1

Since the broadcasting behavior, the protocol does not have the specification about 'response message'. Any messages are delivered to all participants and implicitly done. The sender cannot know any receiver information such as 'properly received' or 'how many participants are accepted the message'.

Although the message layer does not specifies neither response message nor unicast, higher layer virtually provides it. Some messages behave as 'request' and 'response to the request' in semantic view (of course the 2 messages are not related in message layer). See 'prop\_list\_get' and 'prop\_list\_update' as example.

In another situation, the helper system can simulate unicast message by following way.

```
               +-----------------+ ----> uim-toolbar-gtk
uim app1 <---- |uim-helper-server| ----> uim app2
uim app3 ----> +-----------------+ ----> uim configuration tool
        focus_in
```

(1) uim app3 send focus\_in message to declare that "I've activated"

```
                                prop_activate
               +-----------------+ <---- uim-toolbar-gtk
uim app1 <---- |uim-helper-server| ----> uim app2
uim app3 <---- +-----------------+ ----> uim configuration tool
```

(2) uim-toolbar-gtk send prop\_activate

```
                                  prop_activate
                 +-----------------+ <---- uim-toolbar-gtk
  uim app1 x---- |uim-helper-server| ----x uim app2
  uim app3 <---- +-----------------+ ----x uim configuration tool
```

(3) inactive processes ignore the message

All messages in the protocol are defined as follows.

## Message format in (extended) BNF ##

The protocol data consist of human readable messages on an IPC connection. Each messages are consist of arbitrary lines of text and delimited from another message by "\n\n".

```
session  = messages
messages = messages message | message
message  = (focus_in            |
            focus_out           |
            prop_activate       |
            prop_list_get       |
            prop_list_update    |
            im_list             |
            im_list_get         |
            im_change_this_text_area_only   |
            im_change_whole_desktop         |
            im_change_this_application_only |
            prop_update_custom  |
            custom_reload_notify |
            commit_string |
			im_switcher_start
			im_switcher_quit) "\n"

charset_specifier = "charset=" charset "\n"
charset = "UTF-8" | "EUC-JP" | "GB18030" |
          <or any name that can be specified as iconv_open(3) argument>
str = str <any characters except for '\0', '\t' or '\n'> | ""
identifier = [_a-zA-Z][_a-zA-Z0-9]*
```

## Focus notification messages ##

### focus\_in ###

This message declares that the sender has gotten a focus. This means that the focused context of this process has become 'active context' and any other contexts have become 'inactive context'. It implies that only active context can respond to some messages prop\_list\_get, prop\_label\_get, prop\_activate, im\_list\_get and commit\_string. Contexts in other processes have to become inactive by receiving focus\_in message from another process.

Invoke uim\_helper\_client\_focus\_in() to send this message.

```
focus_in = "focus_in\n"
```

### focus\_out ###

This message notifies that the sender has been lost a focus. This message is currently not received by official uim suites.

Invoke uim\_helper\_client\_focus\_out() to send this message.

```
focus_out = "focus_out\n"
```

## Property messages ##

The concept 'property' in uim means 'properties of input method'. An input method (in accurately, input context) can own arbitrary number of properties. A property is ordinarily appeared for user as a popup menu with an indicator. Such indicator will be appeared simultaneously for user if the input method has 2 or more properties. One property controls one variable state of the input method such as 'input mode' or 'keymap'.

```
action_id = identifier
```

### prop\_activate ###

This message notifies that a command named as action\_id has been activated. This message is usually sent from toolbar applets in response to an user selection and received by corresponding IM. Once received, the prop-handler of current IM has been invoked with action\_id. Several IMs use action\_id as 'input mode' such as 'hiragana', 'katakana', 'direct' and so on, and switches to activated input mode on receiving.

See also prop\_list\_update.

```
prop_activate = "prop_activate\n" action_id "\n"
```

### prop\_list\_get ###

This message requests a prop\_list\_update. The request sender will receive prop\_list\_update in response to this message. This message is typically used for active acquiring of prop\_list by toolber applets at start up. If this message has not been sent, the applet has to passively wait for prop\_list\_update that will be notified by current IM to show correct information.

Invoke uim\_helper\_client\_get\_prop\_list() to send this message.

See also prop\_list\_update

```
prop_list_get = "prop_list_get\n"
```

### prop\_list\_update ###

This message notifies that a set of menu items typically for toolbar applets. A message is consist of branches which contains arbitrary number of leaves. A branch represents a property which is shown as (popup) menu for user, and a leaf represents a menu item of the branch.

indication\_id is an identifier that specifies visual appearance of the item. The ID roughly considerable as "icon name", and so the message receiver can use it to form filename for the corresponding icon (e.g. "anthy" -> "/path/to/somewhere/32x32/anthy.png"). There is a special ID. If the ID is "separator", message receivers should display the leaf as toolkit-native separator. But it is not necessary since the "separator" appears as dummy item with no action if the receiver is not aware of it.

iconic\_label is a very short string typically 1 character to be used as icon. For example, "a" means 'direct input'. This field should be translated with gettext(3) or equivalent. See safe\_gettext() of toolbar-common-gtk.c.

label\_string is a short string to be shown in the menu, or used as tooltip of the button. This field should be translated with gettext(3) or equivalent.

short\_desc is a short description string usually used as tooltip of the menu item. This field should be translated with gettext(3) or equivalent.

action\_id is an identifier of the menu item. This will be notified to other processes by prop\_activate when this menu item has been selected by user.

activity means that whether this menu item is selected. Only one menu item per branch should be notified as "**" which means 'selected'.**

Invoke im-update-prop-list to send this message.

See also prop\_activate.

```
prop_list_update = "prop_list_update\n" charset_specifier parts
parts = parts part | part
part = branch leaves
branch = "branch\t" indication_id "\t" iconic_label "\t" label_string "\n"
leaves = leaves leaf | leaf
leaf = "leaf\t" indication_id "\t" iconic_label "\t"
       label_string "\t" short_desc "\t" action_id "\t" activity "\n"

indication_id = identifier | "separator"
iconic_label = str
label_string = str
short_desc = str
activity = "*" | ""
```

## IM management messages ##

imname is an identifier name of the input method written in ASCII.

```
imname = str
```

### im\_list ###

This message notifies that the set of currently available input methods.

imlang is an i18n-ized free format human readable string such as "Japanese".

imshort\_description is a short description of the input method. This string is currently not i18n-ized (i.e. written in English).

selectedflag specifies which input method of all available one is currently selected. At most one input method has the value "selected".

See also im\_list\_get

```
im_list = "im_list\n" charset_specifier iminfos
iminfos = iminfos iminfo | iminfo
iminfo = imname "\t" imlang "\t" imshort_description "\t" selectedflag"\n"
imlang = human_readable_language_name
imshort_description = str
selectedflag = "selected" | ""
human_readable_language_name = str
```

### im\_list\_get ###

This message requests a im\_list. The request sender will receive im\_list from currently focused input context in response to this message. This message is typically used for active acquiring of im\_list by im-switcher application (such as uim-im-switcher) at start up.

See also im\_list, focus\_in

```
im_list_get = "im_list_get\n"
```

### im\_change\_this\_text\_area\_only ###

This message notifies that currently focused input context must be switched its input method to specified imname. All receivers must properly accept or discard this message in accordance with focus management.

See also focus\_in

```
im_change_this_text_area_only = "im_change_this_text_area_only\n" imname "\n"
```

### im\_change\_this\_application\_only ###

This message notifies that all input context of the application that has currently focused input context must be switched its input method to specified imname. All receiver processes must properly accept or discard this message in accordance with focus management.

See also focus\_in

```
im_change_this_application_only = "im_change_this_application_only\n" imname "\n"
```

### im\_change\_whole\_desktop ###

This message notifies that all input contexts in local machine must be switched its input method to specified imname. All receiver processes must accept this message and switch all input context of the process.

```
im_change_whole_desktop = "im_change_whole_desktop\n" imname "\n"
```

## Other messages ##

### prop\_update\_custom ###

Update a custom value of received process. The received message are evaluated as (custom-set! custom\_sym custom\_value) and immediately affects the running IMs. Both custom\_sym and custom\_value will be strictly validated to prevent crashing or abuse. Invalid messages will be simply ignored.

custom\_sym and custom\_value are delimited by "\n" instead of "\t" to allow "\t" to be included in the value.

The command name 'prop\_update\_custom' is wrongly named by misunderstanding about naming convention of the helper protocol. It should be renamed as 'custom\_set'.

```
prop_update_custom = "prop_update_custom\n" custom_sym "\n" custom_value "\n"
custom_sym = /^[-\?a-zA-Z0-9]+$/
custom_value = <valid S-expression>
```

### custom\_reload\_notify ###

This is a notification message to reload configrations. If a process receive this message, the process should reload configrations somehow. This message maybe needless in the future.

```
custom_reload_notify = "custom_reload_notify\n"
```

### commit\_string ###

This message commits a string to currently focused context. See also focus\_in.

```
commit_string = "commit_string\n" charset_specifier str_to_commit "\n"
str_to_commit = /^[^\n]+$/
```

### im\_switcher\_start ###

This message notifies that a new uim-im-switcher is started.
When an existing old uim-im-switcher receives im\_switcher\_start,
the existing uim-im-switcher must send im\_switcher\_quit
to quit newly started uim-im-switcher.

See also im\_switcher\_quit.

```
im_switcher_start = "im_switcher_start\n"
```

### im\_switcher\_quit ###

This message requests newly started uim-im-switcher to quit.
All uim-im-switcher must quit immediately after received this message.

See also im\_switcher\_start.

```
im_switcher_quit = "im_switcher_quit\n"
```