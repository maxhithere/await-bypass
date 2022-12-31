# await-bypass
use await on top level


This code exports a function that can be used to require a JavaScript file with the async keyword. When this function is called with a path to a JavaScript file and a parent module, it first resolves the filename of the file to be required by calling Module._resolveFilename() with the provided path, parent module, and a boolean flag indicating that the file should not be treated as a system module.

Next, the code checks if the resolved filename has already been cached. If it has, it returns the cached version. If not, the code checks that the file has a .js extension. If it does not, it throws an error.

The code then modifies the Module.wrap function to wrap the script in an async function. It does this by saving the original Module.wrap function, replacing it with a new function that wraps the script in an async function, and then restoring the original Module.wrap function after the wrapping is done.

The code also saves the original Module._extensions['.js'] function and replaces it with a new function that reads the file specified by filename, removes the Byte Order Mark (BOM) if present, and compiles the content using module._compile(). It then restores the original Module._extensions['.js'] function.

Finally, the code calls Module._load() to load the module, and returns a promise that resolves to the exports of the module. The exports are cached in the cache object so that they can be returned if the same file is required again.
