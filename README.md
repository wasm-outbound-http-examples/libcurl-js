# Use libcurl.js to send HTTP(s) requests from inside WASM

This devcontainer is configured to provide you an Emscripten and other tools to compile libcurl.js, and run both server-side (websocket-enabled "proxy") and client side (web server to deliever WASM and glue code to browsers).

[![Open in GitHub Codespaces](https://github.com/codespaces/badge.svg)](https://codespaces.new/wasm-outbound-http-examples/libcurl-js)

The sample code and following instructions are partially based on [libcurl.js docs](https://github.com/ading2210/libcurl.js/blob/main/README.md) and examples.

## Instructions for this devcontainer

Tested with `libcurl.js` [0.6.11](https://github.com/ading2210/libcurl.js/tree/4d64b27a8293de87d7e39b30685ca17ee9c324a3), 
and Emscripten 3.1.6.

### Preparation

1. Open this repo in devcontainer, e.g. using Github Codespaces.
   Type or copy/paste following commands to devcontainer's terminal.

2. Clone the libcurl.js repo:

```sh
git clone https://github.com/ading2210/libcurl.js --recursive --depth=1
```

### Building and running server-side code

1. `cd` to sources of server-side part:

```sh
cd libcurl.js/server
```

2. Run the server-side part:

```sh
./run.sh
```

This will install dependencies if needed (by using `venv`) and start a websocket server.

3. Press `Make Public` button when codespace shows port forwarding confirmation dialog.

### Building browser-side code

1. Open new terminal tab in your codespace, leaving server-side tab running.

2. In new tab, `cd` to sources of client-side part:

```sh
cd libcurl.js/client
```

3. Compile the client-side code, including patched libcurl:

```sh
./build.sh
```

The compilation will take about 5-10 minutes, resulting to 2.8Mb `libcurl.wasm` file in the `out` subfolder,
along with 2 glue JS files.

### Test with browser

Continue to use terminal tab for client side.

1. Copy HTTP-request-enabled example from parent folder instead default one:

```sh
cp ../../index.html ./
```

2. Run simple HTTP server to temporarily publish project to Web:

```sh
python3 -m http.server
```

3. Codespace will show you "Open in Browser" button. Just click that button or
   obtain web address from "Forwarded Ports" tab.

4. As `index.html`, JS files, and a 2.8M-sized `libcurl.wasm` are loaded into browser, refer to browser developer console
   to see the results.


### Finish

Perform your own experiments if desired.
The [`worker.html`](https://github.com/ading2210/libcurl.js/blob/4d64b27a8293de87d7e39b30685ca17ee9c324a3/client/worker.html) is one of the earliest candidates to try.

---

<sub>Created for (wannabe-awesome) [list](https://github.com/vasilev/HTTP-request-from-inside-WASM)</sub>
