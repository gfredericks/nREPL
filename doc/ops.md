<!-- This file is *generated* by #'nrepl.describe-test/update-op-docs
   **Do not edit!** -->
# Supported nREPL operations

<small>generated from a verbose 'describe' response (nREPL v0.2.11-SNAPSHOT)</small>

## Operations

### `:clone`

Clones the current session, returning the ID of the newly-created session.

###### Required parameters



###### Optional parameters

* `:session` The ID of the session to be cloned; if not provided, a new session with default bindings is created, and mapped to the returned session ID.


###### Returns

* `:new-session` The ID of the new session.


### `:close`

Closes the specified session.

###### Required parameters

* `:session` The ID of the session to be closed.


###### Optional parameters



###### Returns



### `:describe`

Produce a machine- and human-readable directory and documentation for the operations supported by an nREPL endpoint.

###### Required parameters



###### Optional parameters

* `:verbose?` Include informational detail for each "op"eration in the return message.


###### Returns

* `:aux` Map of auxilliary data contributed by all of the active nREPL middleware via :describe-fn functions in their descriptors.
* `:ops` Map of "op"erations supported by this nREPL endpoint
* `:versions` Map containing version maps (like \*clojure-version\*, e.g. major, minor, incremental, and qualifier keys) for values, component names as keys. Common keys include "nrepl" and "clojure".


### `:eval`

Evaluates code.

###### Required parameters

* `:code` The code to be evaluated.
* `:session` The ID of the session within which to evaluate the code.


###### Optional parameters

* `:column` The column number in [file] at which [code] starts.
* `:eval` A fully-qualified symbol naming a var whose function value will be used to evaluate [code], instead of `clojure.core/eval` (the default).
* `:file` The path to the file containing [code]. `clojure.core/\*file\*` will be bound to this.
* `:id` An opaque message ID that will be included in responses related to the evaluation, and which may be used to restrict the scope of a later "interrupt" operation.
* `:line` The line number in [file] at which [code] starts.


###### Returns

* `:ex` The type of exception thrown, if any. If present, then `values` will be absent.
* `:ns` \*ns\*, after successful evaluation of `code`.
* `:root-ex` The type of the root exception thrown, if any. If present, then `values` will be absent.
* `:values` The result of evaluating `code`, often `read`able. This printing is provided by the `pr-values` middleware, and could theoretically be customized. Superseded by `ex` and `root-ex` if an exception occurs during evaluation.


### `:interrupt`

Attempts to interrupt some code evaluation.

###### Required parameters

* `:session` The ID of the session used to start the evaluation to be interrupted.


###### Optional parameters

* `:interrupt-id` The opaque message ID sent with the original "eval" request.


###### Returns

* `:status` 'interrupted' if an evaluation was identified and interruption will be attempted
'session-idle' if the session is not currently evaluating any code
'interrupt-id-mismatch' if the session is currently evaluating code sent using a different ID than specified by the "interrupt-id" value


### `:load-file`

Loads a body of code, using supplied path and filename info to set source file and line number metadata. Delegates to underlying "eval" middleware/handler.

###### Required parameters

* `:file` Full contents of a file of code.


###### Optional parameters

* `:file-name` Name of source file, e.g. io.clj
* `:file-path` Source-path-relative path of the source file, e.g. clojure/java/io.clj


###### Returns

* `:ex` The type of exception thrown, if any. If present, then `values` will be absent.
* `:ns` \*ns\*, after successful evaluation of `code`.
* `:root-ex` The type of the root exception thrown, if any. If present, then `values` will be absent.
* `:values` The result of evaluating `code`, often `read`able. This printing is provided by the `pr-values` middleware, and could theoretically be customized. Superseded by `ex` and `root-ex` if an exception occurs during evaluation.


### `:ls-sessions`

Lists the IDs of all active sessions.

###### Required parameters



###### Optional parameters



###### Returns

* `:sessions` A list of all available session IDs.


### `:stdin`

Add content from the value of "stdin" to \*in\* in the current session.

###### Required parameters

* `:stdin` Content to add to \*in\*.


###### Optional parameters



###### Returns

* `:status` A status of "need-input" will be sent if a session's \*in\* requires content in order to satisfy an attempted read operation.
