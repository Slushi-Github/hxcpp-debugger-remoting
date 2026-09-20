# HXCPP Debugger - Remote Debugging

This VSCode extension allows you to debug [HXCPP](https://haxe.org/manual/target-cpp-getting-started.html) applications.

Modified to support remote connections from a remote device.

## Usage

To debug a HXCPP application, it needs to be compiled with the `hxcpp-debug-server` library and in debug mode. First, run the "HXCPP: Setup" command from the command palette (<kbd>F1</kbd>) to install the library.

Then the library needs to be included in your project:

* `build.hxml`:

	```
	-lib hxcpp-debug-server
	```

* Lime/OpenFL `project.xml`:

	```
	<haxelib name="hxcpp-debug-server" />
	```

And you need define the host of the server (where the debugger will connect to) in your project:

* `build.hxml`:

    ```
    -D HXCPP_DEBUG_HOST=192.168.1.10
    ```

* Lime/OpenFL `project.xml`:

    ```
    <define name="HXCPP_DEBUG_HOST" value="192.168.1.10" />
    ```
    
Replace `192.168.1.10` with the IP address of the server on which the server will run.

Finally, you need a launch configuration:

```json
{ 
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Remote Debug",
            "type": "hxcpp",
            "request": "launch",
            "remote": true,
            "clientIP": "192.168.1.50"
        }
    ]
}
```

Replace `192.168.1.50` with the IP address of your device.

(The default method of using a local executable is still supported, I just show how to use a remote one.)

## Installing from source

1. Navigate to the extensions folder (`C:\Users\<username>\.vscode\extensions` on Windows, `~/.vscode/extensions` otherwise)
2. Clone this repo: `git clone https://github.com/Slushi-GitHub/hxcpp-debugger`
3. Change current directory to the cloned one: `cd hxcpp-debugger`.
4. Install dependencies `npm install`
5. Do `npx haxe build.hxml`
