#Code School Console
This console was designed to take advantage of code mirrors excellent key input
and code highlight ability. The idea is that we should let code mirror handle all
the hard key input stuff while we focus on the console ui. We can also use any
code mirror addon/plugin out there.


##Dependancies:
* CodeMirror:
    - vibrant-ink theme
    - Code Mirror 2 Editor

##Usage:
  You can Instantiate CSConsole and pass a variety of options to customize the console
  functionality.

###Options:
* **prompt** - Sets the console prompt, this can be anything
* **initialValue** - Sets the initialValue of the console input field
* **historyLabel** - Sets a label for the localStorage history. This should be set if you don't want consoles from different applications to share history
* **welcomeMessage** - An initial message at the top of the console when it first loads
* **autoFocus** - Whether or not the console should be focused on page load.
* **commandValidate** - Callback function for validating a command before it's submitted. This callback should return a boolean
* **commandHandle** - Callback function for handling a command. This callback is passed the following arguments:
    - ***inputContent*** - This is the content of the input
    - ***responder*** - The responder is used to send some sort of a response to the console. This can be an asyncronous response. The className sets a class name on the html element of the output widget. The content can be either a string, or a valid HTMLElement. *Note, this is not a jQuery object*.

        Also, the console will not enter a state where it is ready for another command unless this responder has been called. If you want to implement a command that does not have any output Something like 'next' for progressing through course levels, then make sure to call the responder passing a falsy value(or nothing) The format of this response can be either an array of objects or a single object.
        **Example:**

        ```ruby
        [
            {content: "Blah blah output\noutput", className: 'console-output'},
            {content: "Blah blah output\noutput", className: 'console-error'}
        ]
        ```




* **prompt** - This is the value of the prompt set in the editor.
* **cancelHandle** - This callback is called when a command is canceled. This is currently
                   not implemented.
* **theme** - Set the code mirror theme, defaults to 'vibrant-ink'

* **lineNumbers** - Enables line numbers, defaults to false

##Methods
* **setValue(string)** - Set the value of the input line
* **getValue** - Get the value of the input, this includes multiline input
* **setPrompt(string)** - Set the prompt
* **reset(prompt)** - Clear the console, pass false to this method to not display the welcome message.
* **buildWidget(lineNumber, responseObject)** - Manually create a output widget. This requires a lineNumber and a response object like the one used in the commandHandle callback Method above.
* **innerConsole** - Return the CodeMirror instance used within the console, useful for low level interface functionality.
* **focus** - Focus the input typer box
* **appendToInput** - Append a value to the typer box


##Misc tips and troubles
If you find that the console gets stuck in a state where the prompt isn't being displayed
and it's not responding to input, make sure that responder is called in your 'commandHandle'
callback at some point. If you don't want to display any output just call the responder with
an empty or falsy argument to force the console to ready itself for more input.
