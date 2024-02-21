<h1><a name="http_service">World http-service</a></h1>
<p>The <a href="#http_service"><code>http-service</code></a> world is a world that exports a single HTTP
handler that can be used to handle HTTP requests, and
a set of capabilities that can be used to interact with
the platform / runtime.</p>
<ul>
<li>Imports:
<ul>
<li>interface <a href="#wasi:io_error_0.2.0"><code>wasi:io/error@0.2.0</code></a></li>
<li>interface <a href="#wasi:io_poll_0.2.0"><code>wasi:io/poll@0.2.0</code></a></li>
<li>interface <a href="#wasi:io_streams_0.2.0"><code>wasi:io/streams@0.2.0</code></a></li>
<li>interface <a href="#wasi:keyvalue_wasi_keyvalue_error_0.2.0_draft"><code>wasi:keyvalue/wasi-keyvalue-error@0.2.0-draft</code></a></li>
<li>interface <a href="#wasi:keyvalue_types_0.2.0_draft"><code>wasi:keyvalue/types@0.2.0-draft</code></a></li>
<li>interface <a href="#wasi:keyvalue_eventual_0.2.0_draft"><code>wasi:keyvalue/eventual@0.2.0-draft</code></a></li>
<li>interface <a href="#wasi:keyvalue_atomic_0.2.0_draft"><code>wasi:keyvalue/atomic@0.2.0-draft</code></a></li>
<li>interface <a href="#wasi:keyvalue_eventual_batch_0.2.0_draft"><code>wasi:keyvalue/eventual-batch@0.2.0-draft</code></a></li>
<li>interface <a href="#wasi:blobstore_types_0.2.0_draft"><code>wasi:blobstore/types@0.2.0-draft</code></a></li>
<li>interface <a href="#wasi:blobstore_container_0.2.0_draft"><code>wasi:blobstore/container@0.2.0-draft</code></a></li>
<li>interface <a href="#wasi:blobstore_blobstore_0.2.0_draft"><code>wasi:blobstore/blobstore@0.2.0-draft</code></a></li>
<li>interface <a href="#wasi:messaging_messaging_types_0.2.0_draft"><code>wasi:messaging/messaging-types@0.2.0-draft</code></a></li>
<li>interface <a href="#wasi:messaging_producer_0.2.0_draft"><code>wasi:messaging/producer@0.2.0-draft</code></a></li>
<li>interface <a href="#wasi:messaging_consumer_0.2.0_draft"><code>wasi:messaging/consumer@0.2.0-draft</code></a></li>
<li>interface <a href="#wasi:sql_types_0.2.0_draft"><code>wasi:sql/types@0.2.0-draft</code></a></li>
<li>interface <a href="#wasi:sql_readwrite_0.2.0_draft"><code>wasi:sql/readwrite@0.2.0-draft</code></a></li>
<li>interface <a href="#wasi:config_runtime_0.2.0_draft"><code>wasi:config/runtime@0.2.0-draft</code></a></li>
<li>interface <a href="#wasi:random_random_0.2.0"><code>wasi:random/random@0.2.0</code></a></li>
<li>interface <a href="#wasi:cli_stdout_0.2.0"><code>wasi:cli/stdout@0.2.0</code></a></li>
<li>interface <a href="#wasi:cli_stderr_0.2.0"><code>wasi:cli/stderr@0.2.0</code></a></li>
<li>interface <a href="#wasi:cli_stdin_0.2.0"><code>wasi:cli/stdin@0.2.0</code></a></li>
<li>interface <a href="#wasi:clocks_monotonic_clock_0.2.0"><code>wasi:clocks/monotonic-clock@0.2.0</code></a></li>
<li>interface <a href="#wasi:http_types_0.2.0"><code>wasi:http/types@0.2.0</code></a></li>
<li>interface <a href="#wasi:http_outgoing_handler_0.2.0"><code>wasi:http/outgoing-handler@0.2.0</code></a></li>
<li>interface <a href="#wasi:clocks_wall_clock_0.2.0"><code>wasi:clocks/wall-clock@0.2.0</code></a></li>
</ul>
</li>
<li>Exports:
<ul>
<li>interface <a href="#wasi:http_incoming_handler_0.2.0"><code>wasi:http/incoming-handler@0.2.0</code></a></li>
</ul>
</li>
</ul>
<h2><a name="wasi:io_error_0.2.0"></a>Import interface wasi:io/error@0.2.0</h2>
<hr />
<h3>Types</h3>
<h4><a name="error"></a><code>resource error</code></h4>
<p>A resource which represents some error information.</p>
<p>The only method provided by this resource is <code>to-debug-string</code>,
which provides some human-readable information about the error.</p>
<p>In the <code>wasi:io</code> package, this resource is returned through the
<code>wasi:io/streams/stream-error</code> type.</p>
<p>To provide more specific error information, other interfaces may
provide functions to further &quot;downcast&quot; this error into more specific
error information. For example, <a href="#error"><code>error</code></a>s returned in streams derived
from filesystem types to be described using the filesystem's own
error-code type, using the function
<code>wasi:filesystem/types/filesystem-error-code</code>, which takes a parameter
<code>borrow&lt;error&gt;</code> and returns
<code>option&lt;wasi:filesystem/types/error-code&gt;</code>.</p>
<h2>The set of functions which can &quot;downcast&quot; an <a href="#error"><code>error</code></a> into a more
concrete type is open.</h2>
<h3>Functions</h3>
<h4><a name="method_error.to_debug_string"></a><code>[method]error.to-debug-string: func</code></h4>
<p>Returns a string that is suitable to assist humans in debugging
this error.</p>
<p>WARNING: The returned string should not be consumed mechanically!
It may change across platforms, hosts, or other implementation
details. Parsing this string is a major platform-compatibility
hazard.</p>
<h5>Params</h5>
<ul>
<li><a name="method_error.to_debug_string.self"></a><code>self</code>: borrow&lt;<a href="#error"><a href="#error"><code>error</code></a></a>&gt;</li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="method_error.to_debug_string.0"></a> <code>string</code></li>
</ul>
<h2><a name="wasi:io_poll_0.2.0"></a>Import interface wasi:io/poll@0.2.0</h2>
<p>A poll API intended to let users wait for I/O events on multiple handles
at once.</p>
<hr />
<h3>Types</h3>
<h4><a name="pollable"></a><code>resource pollable</code></h4>
<h2><a href="#pollable"><code>pollable</code></a> represents a single I/O event which may be ready, or not.</h2>
<h3>Functions</h3>
<h4><a name="method_pollable.ready"></a><code>[method]pollable.ready: func</code></h4>
<p>Return the readiness of a pollable. This function never blocks.</p>
<p>Returns <code>true</code> when the pollable is ready, and <code>false</code> otherwise.</p>
<h5>Params</h5>
<ul>
<li><a name="method_pollable.ready.self"></a><code>self</code>: borrow&lt;<a href="#pollable"><a href="#pollable"><code>pollable</code></a></a>&gt;</li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="method_pollable.ready.0"></a> <code>bool</code></li>
</ul>
<h4><a name="method_pollable.block"></a><code>[method]pollable.block: func</code></h4>
<p><code>block</code> returns immediately if the pollable is ready, and otherwise
blocks until ready.</p>
<p>This function is equivalent to calling <code>poll.poll</code> on a list
containing only this pollable.</p>
<h5>Params</h5>
<ul>
<li><a name="method_pollable.block.self"></a><code>self</code>: borrow&lt;<a href="#pollable"><a href="#pollable"><code>pollable</code></a></a>&gt;</li>
</ul>
<h4><a name="poll"></a><code>poll: func</code></h4>
<p>Poll for completion on a set of pollables.</p>
<p>This function takes a list of pollables, which identify I/O sources of
interest, and waits until one or more of the events is ready for I/O.</p>
<p>The result <code>list&lt;u32&gt;</code> contains one or more indices of handles in the
argument list that is ready for I/O.</p>
<p>If the list contains more elements than can be indexed with a <code>u32</code>
value, this function traps.</p>
<p>A timeout can be implemented by adding a pollable from the
wasi-clocks API to the list.</p>
<p>This function does not return a <code>result</code>; polling in itself does not
do any I/O so it doesn't fail. If any of the I/O sources identified by
the pollables has an error, it is indicated by marking the source as
being reaedy for I/O.</p>
<h5>Params</h5>
<ul>
<li><a name="poll.in"></a><code>in</code>: list&lt;borrow&lt;<a href="#pollable"><a href="#pollable"><code>pollable</code></a></a>&gt;&gt;</li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="poll.0"></a> list&lt;<code>u32</code>&gt;</li>
</ul>
<h2><a name="wasi:io_streams_0.2.0"></a>Import interface wasi:io/streams@0.2.0</h2>
<p>WASI I/O is an I/O abstraction API which is currently focused on providing
stream types.</p>
<p>In the future, the component model is expected to add built-in stream types;
when it does, they are expected to subsume this API.</p>
<hr />
<h3>Types</h3>
<h4><a name="error"></a><code>type error</code></h4>
<p><a href="#error"><a href="#error"><code>error</code></a></a></p>
<p>
#### <a name="pollable"></a>`type pollable`
[`pollable`](#pollable)
<p>
#### <a name="stream_error"></a>`variant stream-error`
<p>An error for input-stream and output-stream operations.</p>
<h5>Variant Cases</h5>
<ul>
<li>
<p><a name="stream_error.last_operation_failed"></a><code>last-operation-failed</code>: own&lt;<a href="#error"><a href="#error"><code>error</code></a></a>&gt;</p>
<p>The last operation (a write or flush) failed before completion.
<p>More information is available in the <a href="#error"><code>error</code></a> payload.</p>
</li>
<li>
<p><a name="stream_error.closed"></a><code>closed</code></p>
<p>The stream is closed: no more input will be accepted by the
stream. A closed output-stream will return this error on all
future operations.
</li>
</ul>
<h4><a name="input_stream"></a><code>resource input-stream</code></h4>
<p>An input bytestream.</p>
<p><a href="#input_stream"><code>input-stream</code></a>s are <em>non-blocking</em> to the extent practical on underlying
platforms. I/O operations always return promptly; if fewer bytes are
promptly available than requested, they return the number of bytes promptly
available, which could even be zero. To wait for data to be available,
use the <code>subscribe</code> function to obtain a <a href="#pollable"><code>pollable</code></a> which can be polled
for using <code>wasi:io/poll</code>.</p>
<h4><a name="output_stream"></a><code>resource output-stream</code></h4>
<p>An output bytestream.</p>
<h2><a href="#output_stream"><code>output-stream</code></a>s are <em>non-blocking</em> to the extent practical on
underlying platforms. Except where specified otherwise, I/O operations also
always return promptly, after the number of bytes that can be written
promptly, which could even be zero. To wait for the stream to be ready to
accept data, the <code>subscribe</code> function to obtain a <a href="#pollable"><code>pollable</code></a> which can be
polled for using <code>wasi:io/poll</code>.</h2>
<h3>Functions</h3>
<h4><a name="method_input_stream.read"></a><code>[method]input-stream.read: func</code></h4>
<p>Perform a non-blocking read from the stream.</p>
<p>When the source of a <code>read</code> is binary data, the bytes from the source
are returned verbatim. When the source of a <code>read</code> is known to the
implementation to be text, bytes containing the UTF-8 encoding of the
text are returned.</p>
<p>This function returns a list of bytes containing the read data,
when successful. The returned list will contain up to <code>len</code> bytes;
it may return fewer than requested, but not more. The list is
empty when no bytes are available for reading at this time. The
pollable given by <code>subscribe</code> will be ready when more bytes are
available.</p>
<p>This function fails with a <a href="#stream_error"><code>stream-error</code></a> when the operation
encounters an error, giving <code>last-operation-failed</code>, or when the
stream is closed, giving <code>closed</code>.</p>
<p>When the caller gives a <code>len</code> of 0, it represents a request to
read 0 bytes. If the stream is still open, this call should
succeed and return an empty list, or otherwise fail with <code>closed</code>.</p>
<p>The <code>len</code> parameter is a <code>u64</code>, which could represent a list of u8 which
is not possible to allocate in wasm32, or not desirable to allocate as
as a return value by the callee. The callee may return a list of bytes
less than <code>len</code> in size while more bytes are available for reading.</p>
<h5>Params</h5>
<ul>
<li><a name="method_input_stream.read.self"></a><code>self</code>: borrow&lt;<a href="#input_stream"><a href="#input_stream"><code>input-stream</code></a></a>&gt;</li>
<li><a name="method_input_stream.read.len"></a><code>len</code>: <code>u64</code></li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="method_input_stream.read.0"></a> result&lt;list&lt;<code>u8</code>&gt;, <a href="#stream_error"><a href="#stream_error"><code>stream-error</code></a></a>&gt;</li>
</ul>
<h4><a name="method_input_stream.blocking_read"></a><code>[method]input-stream.blocking-read: func</code></h4>
<p>Read bytes from a stream, after blocking until at least one byte can
be read. Except for blocking, behavior is identical to <code>read</code>.</p>
<h5>Params</h5>
<ul>
<li><a name="method_input_stream.blocking_read.self"></a><code>self</code>: borrow&lt;<a href="#input_stream"><a href="#input_stream"><code>input-stream</code></a></a>&gt;</li>
<li><a name="method_input_stream.blocking_read.len"></a><code>len</code>: <code>u64</code></li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="method_input_stream.blocking_read.0"></a> result&lt;list&lt;<code>u8</code>&gt;, <a href="#stream_error"><a href="#stream_error"><code>stream-error</code></a></a>&gt;</li>
</ul>
<h4><a name="method_input_stream.skip"></a><code>[method]input-stream.skip: func</code></h4>
<p>Skip bytes from a stream. Returns number of bytes skipped.</p>
<p>Behaves identical to <code>read</code>, except instead of returning a list
of bytes, returns the number of bytes consumed from the stream.</p>
<h5>Params</h5>
<ul>
<li><a name="method_input_stream.skip.self"></a><code>self</code>: borrow&lt;<a href="#input_stream"><a href="#input_stream"><code>input-stream</code></a></a>&gt;</li>
<li><a name="method_input_stream.skip.len"></a><code>len</code>: <code>u64</code></li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="method_input_stream.skip.0"></a> result&lt;<code>u64</code>, <a href="#stream_error"><a href="#stream_error"><code>stream-error</code></a></a>&gt;</li>
</ul>
<h4><a name="method_input_stream.blocking_skip"></a><code>[method]input-stream.blocking-skip: func</code></h4>
<p>Skip bytes from a stream, after blocking until at least one byte
can be skipped. Except for blocking behavior, identical to <code>skip</code>.</p>
<h5>Params</h5>
<ul>
<li><a name="method_input_stream.blocking_skip.self"></a><code>self</code>: borrow&lt;<a href="#input_stream"><a href="#input_stream"><code>input-stream</code></a></a>&gt;</li>
<li><a name="method_input_stream.blocking_skip.len"></a><code>len</code>: <code>u64</code></li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="method_input_stream.blocking_skip.0"></a> result&lt;<code>u64</code>, <a href="#stream_error"><a href="#stream_error"><code>stream-error</code></a></a>&gt;</li>
</ul>
<h4><a name="method_input_stream.subscribe"></a><code>[method]input-stream.subscribe: func</code></h4>
<p>Create a <a href="#pollable"><code>pollable</code></a> which will resolve once either the specified stream
has bytes available to read or the other end of the stream has been
closed.
The created <a href="#pollable"><code>pollable</code></a> is a child resource of the <a href="#input_stream"><code>input-stream</code></a>.
Implementations may trap if the <a href="#input_stream"><code>input-stream</code></a> is dropped before
all derived <a href="#pollable"><code>pollable</code></a>s created with this function are dropped.</p>
<h5>Params</h5>
<ul>
<li><a name="method_input_stream.subscribe.self"></a><code>self</code>: borrow&lt;<a href="#input_stream"><a href="#input_stream"><code>input-stream</code></a></a>&gt;</li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="method_input_stream.subscribe.0"></a> own&lt;<a href="#pollable"><a href="#pollable"><code>pollable</code></a></a>&gt;</li>
</ul>
<h4><a name="method_output_stream.check_write"></a><code>[method]output-stream.check-write: func</code></h4>
<p>Check readiness for writing. This function never blocks.</p>
<p>Returns the number of bytes permitted for the next call to <code>write</code>,
or an error. Calling <code>write</code> with more bytes than this function has
permitted will trap.</p>
<p>When this function returns 0 bytes, the <code>subscribe</code> pollable will
become ready when this function will report at least 1 byte, or an
error.</p>
<h5>Params</h5>
<ul>
<li><a name="method_output_stream.check_write.self"></a><code>self</code>: borrow&lt;<a href="#output_stream"><a href="#output_stream"><code>output-stream</code></a></a>&gt;</li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="method_output_stream.check_write.0"></a> result&lt;<code>u64</code>, <a href="#stream_error"><a href="#stream_error"><code>stream-error</code></a></a>&gt;</li>
</ul>
<h4><a name="method_output_stream.write"></a><code>[method]output-stream.write: func</code></h4>
<p>Perform a write. This function never blocks.</p>
<p>When the destination of a <code>write</code> is binary data, the bytes from
<code>contents</code> are written verbatim. When the destination of a <code>write</code> is
known to the implementation to be text, the bytes of <code>contents</code> are
transcoded from UTF-8 into the encoding of the destination and then
written.</p>
<p>Precondition: check-write gave permit of Ok(n) and contents has a
length of less than or equal to n. Otherwise, this function will trap.</p>
<p>returns Err(closed) without writing if the stream has closed since
the last call to check-write provided a permit.</p>
<h5>Params</h5>
<ul>
<li><a name="method_output_stream.write.self"></a><code>self</code>: borrow&lt;<a href="#output_stream"><a href="#output_stream"><code>output-stream</code></a></a>&gt;</li>
<li><a name="method_output_stream.write.contents"></a><code>contents</code>: list&lt;<code>u8</code>&gt;</li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="method_output_stream.write.0"></a> result&lt;_, <a href="#stream_error"><a href="#stream_error"><code>stream-error</code></a></a>&gt;</li>
</ul>
<h4><a name="method_output_stream.blocking_write_and_flush"></a><code>[method]output-stream.blocking-write-and-flush: func</code></h4>
<p>Perform a write of up to 4096 bytes, and then flush the stream. Block
until all of these operations are complete, or an error occurs.</p>
<p>This is a convenience wrapper around the use of <code>check-write</code>,
<code>subscribe</code>, <code>write</code>, and <code>flush</code>, and is implemented with the
following pseudo-code:</p>
<pre><code class="language-text">let pollable = this.subscribe();
while !contents.is_empty() {
  // Wait for the stream to become writable
  pollable.block();
  let Ok(n) = this.check-write(); // eliding error handling
  let len = min(n, contents.len());
  let (chunk, rest) = contents.split_at(len);
  this.write(chunk  );            // eliding error handling
  contents = rest;
}
this.flush();
// Wait for completion of `flush`
pollable.block();
// Check for any errors that arose during `flush`
let _ = this.check-write();         // eliding error handling
</code></pre>
<h5>Params</h5>
<ul>
<li><a name="method_output_stream.blocking_write_and_flush.self"></a><code>self</code>: borrow&lt;<a href="#output_stream"><a href="#output_stream"><code>output-stream</code></a></a>&gt;</li>
<li><a name="method_output_stream.blocking_write_and_flush.contents"></a><code>contents</code>: list&lt;<code>u8</code>&gt;</li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="method_output_stream.blocking_write_and_flush.0"></a> result&lt;_, <a href="#stream_error"><a href="#stream_error"><code>stream-error</code></a></a>&gt;</li>
</ul>
<h4><a name="method_output_stream.flush"></a><code>[method]output-stream.flush: func</code></h4>
<p>Request to flush buffered output. This function never blocks.</p>
<p>This tells the output-stream that the caller intends any buffered
output to be flushed. the output which is expected to be flushed
is all that has been passed to <code>write</code> prior to this call.</p>
<p>Upon calling this function, the <a href="#output_stream"><code>output-stream</code></a> will not accept any
writes (<code>check-write</code> will return <code>ok(0)</code>) until the flush has
completed. The <code>subscribe</code> pollable will become ready when the
flush has completed and the stream can accept more writes.</p>
<h5>Params</h5>
<ul>
<li><a name="method_output_stream.flush.self"></a><code>self</code>: borrow&lt;<a href="#output_stream"><a href="#output_stream"><code>output-stream</code></a></a>&gt;</li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="method_output_stream.flush.0"></a> result&lt;_, <a href="#stream_error"><a href="#stream_error"><code>stream-error</code></a></a>&gt;</li>
</ul>
<h4><a name="method_output_stream.blocking_flush"></a><code>[method]output-stream.blocking-flush: func</code></h4>
<p>Request to flush buffered output, and block until flush completes
and stream is ready for writing again.</p>
<h5>Params</h5>
<ul>
<li><a name="method_output_stream.blocking_flush.self"></a><code>self</code>: borrow&lt;<a href="#output_stream"><a href="#output_stream"><code>output-stream</code></a></a>&gt;</li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="method_output_stream.blocking_flush.0"></a> result&lt;_, <a href="#stream_error"><a href="#stream_error"><code>stream-error</code></a></a>&gt;</li>
</ul>
<h4><a name="method_output_stream.subscribe"></a><code>[method]output-stream.subscribe: func</code></h4>
<p>Create a <a href="#pollable"><code>pollable</code></a> which will resolve once the output-stream
is ready for more writing, or an error has occured. When this
pollable is ready, <code>check-write</code> will return <code>ok(n)</code> with n&gt;0, or an
error.</p>
<p>If the stream is closed, this pollable is always ready immediately.</p>
<p>The created <a href="#pollable"><code>pollable</code></a> is a child resource of the <a href="#output_stream"><code>output-stream</code></a>.
Implementations may trap if the <a href="#output_stream"><code>output-stream</code></a> is dropped before
all derived <a href="#pollable"><code>pollable</code></a>s created with this function are dropped.</p>
<h5>Params</h5>
<ul>
<li><a name="method_output_stream.subscribe.self"></a><code>self</code>: borrow&lt;<a href="#output_stream"><a href="#output_stream"><code>output-stream</code></a></a>&gt;</li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="method_output_stream.subscribe.0"></a> own&lt;<a href="#pollable"><a href="#pollable"><code>pollable</code></a></a>&gt;</li>
</ul>
<h4><a name="method_output_stream.write_zeroes"></a><code>[method]output-stream.write-zeroes: func</code></h4>
<p>Write zeroes to a stream.</p>
<p>This should be used precisely like <code>write</code> with the exact same
preconditions (must use check-write first), but instead of
passing a list of bytes, you simply pass the number of zero-bytes
that should be written.</p>
<h5>Params</h5>
<ul>
<li><a name="method_output_stream.write_zeroes.self"></a><code>self</code>: borrow&lt;<a href="#output_stream"><a href="#output_stream"><code>output-stream</code></a></a>&gt;</li>
<li><a name="method_output_stream.write_zeroes.len"></a><code>len</code>: <code>u64</code></li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="method_output_stream.write_zeroes.0"></a> result&lt;_, <a href="#stream_error"><a href="#stream_error"><code>stream-error</code></a></a>&gt;</li>
</ul>
<h4><a name="method_output_stream.blocking_write_zeroes_and_flush"></a><code>[method]output-stream.blocking-write-zeroes-and-flush: func</code></h4>
<p>Perform a write of up to 4096 zeroes, and then flush the stream.
Block until all of these operations are complete, or an error
occurs.</p>
<p>This is a convenience wrapper around the use of <code>check-write</code>,
<code>subscribe</code>, <code>write-zeroes</code>, and <code>flush</code>, and is implemented with
the following pseudo-code:</p>
<pre><code class="language-text">let pollable = this.subscribe();
while num_zeroes != 0 {
  // Wait for the stream to become writable
  pollable.block();
  let Ok(n) = this.check-write(); // eliding error handling
  let len = min(n, num_zeroes);
  this.write-zeroes(len);         // eliding error handling
  num_zeroes -= len;
}
this.flush();
// Wait for completion of `flush`
pollable.block();
// Check for any errors that arose during `flush`
let _ = this.check-write();         // eliding error handling
</code></pre>
<h5>Params</h5>
<ul>
<li><a name="method_output_stream.blocking_write_zeroes_and_flush.self"></a><code>self</code>: borrow&lt;<a href="#output_stream"><a href="#output_stream"><code>output-stream</code></a></a>&gt;</li>
<li><a name="method_output_stream.blocking_write_zeroes_and_flush.len"></a><code>len</code>: <code>u64</code></li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="method_output_stream.blocking_write_zeroes_and_flush.0"></a> result&lt;_, <a href="#stream_error"><a href="#stream_error"><code>stream-error</code></a></a>&gt;</li>
</ul>
<h4><a name="method_output_stream.splice"></a><code>[method]output-stream.splice: func</code></h4>
<p>Read from one stream and write to another.</p>
<p>The behavior of splice is equivelant to:</p>
<ol>
<li>calling <code>check-write</code> on the <a href="#output_stream"><code>output-stream</code></a></li>
<li>calling <code>read</code> on the <a href="#input_stream"><code>input-stream</code></a> with the smaller of the
<code>check-write</code> permitted length and the <code>len</code> provided to <code>splice</code></li>
<li>calling <code>write</code> on the <a href="#output_stream"><code>output-stream</code></a> with that read data.</li>
</ol>
<p>Any error reported by the call to <code>check-write</code>, <code>read</code>, or
<code>write</code> ends the splice and reports that error.</p>
<p>This function returns the number of bytes transferred; it may be less
than <code>len</code>.</p>
<h5>Params</h5>
<ul>
<li><a name="method_output_stream.splice.self"></a><code>self</code>: borrow&lt;<a href="#output_stream"><a href="#output_stream"><code>output-stream</code></a></a>&gt;</li>
<li><a name="method_output_stream.splice.src"></a><code>src</code>: borrow&lt;<a href="#input_stream"><a href="#input_stream"><code>input-stream</code></a></a>&gt;</li>
<li><a name="method_output_stream.splice.len"></a><code>len</code>: <code>u64</code></li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="method_output_stream.splice.0"></a> result&lt;<code>u64</code>, <a href="#stream_error"><a href="#stream_error"><code>stream-error</code></a></a>&gt;</li>
</ul>
<h4><a name="method_output_stream.blocking_splice"></a><code>[method]output-stream.blocking-splice: func</code></h4>
<p>Read from one stream and write to another, with blocking.</p>
<p>This is similar to <code>splice</code>, except that it blocks until the
<a href="#output_stream"><code>output-stream</code></a> is ready for writing, and the <a href="#input_stream"><code>input-stream</code></a>
is ready for reading, before performing the <code>splice</code>.</p>
<h5>Params</h5>
<ul>
<li><a name="method_output_stream.blocking_splice.self"></a><code>self</code>: borrow&lt;<a href="#output_stream"><a href="#output_stream"><code>output-stream</code></a></a>&gt;</li>
<li><a name="method_output_stream.blocking_splice.src"></a><code>src</code>: borrow&lt;<a href="#input_stream"><a href="#input_stream"><code>input-stream</code></a></a>&gt;</li>
<li><a name="method_output_stream.blocking_splice.len"></a><code>len</code>: <code>u64</code></li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="method_output_stream.blocking_splice.0"></a> result&lt;<code>u64</code>, <a href="#stream_error"><a href="#stream_error"><code>stream-error</code></a></a>&gt;</li>
</ul>
<h2><a name="wasi:keyvalue_wasi_keyvalue_error_0.2.0_draft"></a>Import interface wasi:keyvalue/wasi-keyvalue-error@0.2.0-draft</h2>
<hr />
<h3>Types</h3>
<h4><a name="error"></a><code>resource error</code></h4>
<p>An error resource type for keyvalue operations.</p>
<p>Common errors:</p>
<ul>
<li>Connectivity errors (e.g. network errors): when the client cannot establish
a connection to the keyvalue service.</li>
<li>Authentication and Authorization errors: when the client fails to authenticate
or does not have the required permissions to perform the operation.</li>
<li>Data errors: when the client sends incompatible or corrupted data.</li>
<li>Resource errors: when the system runs out of resources (e.g. memory).</li>
<li>Internal errors: unexpected errors on the server side.</li>
</ul>
<h2>Currently, this provides only one function to return a string representation
of the error. In the future, this will be extended to provide more information
about the error.
Soon: switch to <code>resource error { ... }</code></h2>
<h3>Functions</h3>
<h4><a name="method_error.trace"></a><code>[method]error.trace: func</code></h4>
<h5>Params</h5>
<ul>
<li><a name="method_error.trace.self"></a><code>self</code>: borrow&lt;<a href="#error"><a href="#error"><code>error</code></a></a>&gt;</li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="method_error.trace.0"></a> <code>string</code></li>
</ul>
<h2><a name="wasi:keyvalue_types_0.2.0_draft"></a>Import interface wasi:keyvalue/types@0.2.0-draft</h2>
<p>A generic keyvalue interface for WASI.</p>
<hr />
<h3>Types</h3>
<h4><a name="input_stream"></a><code>type input-stream</code></h4>
<p><a href="#input_stream"><a href="#input_stream"><code>input-stream</code></a></a></p>
<p>
#### <a name="output_stream"></a>`type output-stream`
[`output-stream`](#output_stream)
<p>
#### <a name="error"></a>`type error`
[`error`](#error)
<p>
#### <a name="bucket"></a>`resource bucket`
<p>A bucket is a collection of key-value pairs. Each key-value pair is stored
as a entry in the bucket, and the bucket itself acts as a collection of all
these entries.</p>
<p>It is worth noting that the exact terminology for bucket in key-value stores
can very depending on the specific implementation. For example,</p>
<ol>
<li>Amazon DynamoDB calls a collection of key-value pairs a table</li>
<li>Redis has hashes, sets, and sorted sets as different types of collections</li>
<li>Cassandra calls a collection of key-value pairs a column family</li>
<li>MongoDB calls a collection of key-value pairs a collection</li>
<li>Riak calls a collection of key-value pairs a bucket</li>
<li>Memcached calls a collection of key-value pairs a slab</li>
<li>Azure Cosmos DB calls a collection of key-value pairs a container</li>
</ol>
<p>In this interface, we use the term <a href="#bucket"><code>bucket</code></a> to refer to a collection of key-value
Soon: switch to <code>resource bucket { ... }</code></p>
<h4><a name="key"></a><code>type key</code></h4>
<p><code>string</code></p>
<p>A key is a unique identifier for a value in a bucket. The key is used to
retrieve the value from the bucket.
<h4><a name="outgoing_value"></a><code>resource outgoing-value</code></h4>
<p>A value is the data stored in a key-value pair. The value can be of any type
that can be represented in a byte array. It provides a way to write the value
to the output-stream defined in the <code>wasi-io</code> interface.
Soon: switch to <code>resource value { ... }</code></p>
<h4><a name="outgoing_value_body_async"></a><code>type outgoing-value-body-async</code></h4>
<p><a href="#output_stream"><a href="#output_stream"><code>output-stream</code></a></a></p>
<p>
#### <a name="outgoing_value_body_sync"></a>`type outgoing-value-body-sync`
[`outgoing-value-body-sync`](#outgoing_value_body_sync)
<p>
#### <a name="incoming_value"></a>`resource incoming-value`
<p>A incoming-value is a wrapper around a value. It provides a way to read the value
from the <a href="#input_stream"><code>input-stream</code></a> defined in the <code>wasi-io</code> interface.</p>
<p>The incoming-value provides two ways to consume the value:</p>
<ol>
<li><code>incoming-value-consume-sync</code> consumes the value synchronously and returns the
value as a <code>list&lt;u8&gt;</code>.</li>
<li><code>incoming-value-consume-async</code> consumes the value asynchronously and returns the
value as an <a href="#input_stream"><code>input-stream</code></a>.
In addition, it provides a <code>incoming-value-size</code> function to get the size of the value.
This is useful when the value is large and the caller wants to allocate a buffer of
the right size to consume the value.
Soon: switch to <code>resource incoming-value { ... }</code></li>
</ol>
<h4><a name="incoming_value_async_body"></a><code>type incoming-value-async-body</code></h4>
<p><a href="#input_stream"><a href="#input_stream"><code>input-stream</code></a></a></p>
<p>
#### <a name="incoming_value_sync_body"></a>`type incoming-value-sync-body`
[`incoming-value-sync-body`](#incoming_value_sync_body)
<p>
----
<h3>Functions</h3>
<h4><a name="static_bucket.open_bucket"></a><code>[static]bucket.open-bucket: func</code></h4>
<p>Opens a bucket with the given name.</p>
<p>If any error occurs, including if the bucket does not exist, it returns an <code>Err(error)</code>.</p>
<h5>Params</h5>
<ul>
<li><a name="static_bucket.open_bucket.name"></a><code>name</code>: <code>string</code></li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="static_bucket.open_bucket.0"></a> result&lt;own&lt;<a href="#bucket"><a href="#bucket"><code>bucket</code></a></a>&gt;, own&lt;<a href="#error"><a href="#error"><code>error</code></a></a>&gt;&gt;</li>
</ul>
<h4><a name="static_outgoing_value.new_outgoing_value"></a><code>[static]outgoing-value.new-outgoing-value: func</code></h4>
<h5>Return values</h5>
<ul>
<li><a name="static_outgoing_value.new_outgoing_value.0"></a> own&lt;<a href="#outgoing_value"><a href="#outgoing_value"><code>outgoing-value</code></a></a>&gt;</li>
</ul>
<h4><a name="method_outgoing_value.outgoing_value_write_body_async"></a><code>[method]outgoing-value.outgoing-value-write-body-async: func</code></h4>
<p>Writes the value to the output-stream asynchronously.
If any other error occurs, it returns an <code>Err(error)</code>.</p>
<h5>Params</h5>
<ul>
<li><a name="method_outgoing_value.outgoing_value_write_body_async.self"></a><code>self</code>: borrow&lt;<a href="#outgoing_value"><a href="#outgoing_value"><code>outgoing-value</code></a></a>&gt;</li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="method_outgoing_value.outgoing_value_write_body_async.0"></a> result&lt;own&lt;<a href="#outgoing_value_body_async"><a href="#outgoing_value_body_async"><code>outgoing-value-body-async</code></a></a>&gt;, own&lt;<a href="#error"><a href="#error"><code>error</code></a></a>&gt;&gt;</li>
</ul>
<h4><a name="method_outgoing_value.outgoing_value_write_body_sync"></a><code>[method]outgoing-value.outgoing-value-write-body-sync: func</code></h4>
<p>Writes the value to the output-stream synchronously.
If any other error occurs, it returns an <code>Err(error)</code>.</p>
<h5>Params</h5>
<ul>
<li><a name="method_outgoing_value.outgoing_value_write_body_sync.self"></a><code>self</code>: borrow&lt;<a href="#outgoing_value"><a href="#outgoing_value"><code>outgoing-value</code></a></a>&gt;</li>
<li><a name="method_outgoing_value.outgoing_value_write_body_sync.value"></a><code>value</code>: <a href="#outgoing_value_body_sync"><a href="#outgoing_value_body_sync"><code>outgoing-value-body-sync</code></a></a></li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="method_outgoing_value.outgoing_value_write_body_sync.0"></a> result&lt;_, own&lt;<a href="#error"><a href="#error"><code>error</code></a></a>&gt;&gt;</li>
</ul>
<h4><a name="static_incoming_value.incoming_value_consume_sync"></a><code>[static]incoming-value.incoming-value-consume-sync: func</code></h4>
<p>Consumes the value synchronously and returns the value as a list of bytes.
If any other error occurs, it returns an <code>Err(error)</code>.</p>
<h5>Params</h5>
<ul>
<li><a name="static_incoming_value.incoming_value_consume_sync.this"></a><code>this</code>: own&lt;<a href="#incoming_value"><a href="#incoming_value"><code>incoming-value</code></a></a>&gt;</li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="static_incoming_value.incoming_value_consume_sync.0"></a> result&lt;<a href="#incoming_value_sync_body"><a href="#incoming_value_sync_body"><code>incoming-value-sync-body</code></a></a>, own&lt;<a href="#error"><a href="#error"><code>error</code></a></a>&gt;&gt;</li>
</ul>
<h4><a name="static_incoming_value.incoming_value_consume_async"></a><code>[static]incoming-value.incoming-value-consume-async: func</code></h4>
<p>Consumes the value asynchronously and returns the value as an <a href="#input_stream"><code>input-stream</code></a>.
If any other error occurs, it returns an <code>Err(error)</code>.</p>
<h5>Params</h5>
<ul>
<li><a name="static_incoming_value.incoming_value_consume_async.this"></a><code>this</code>: own&lt;<a href="#incoming_value"><a href="#incoming_value"><code>incoming-value</code></a></a>&gt;</li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="static_incoming_value.incoming_value_consume_async.0"></a> result&lt;own&lt;<a href="#incoming_value_async_body"><a href="#incoming_value_async_body"><code>incoming-value-async-body</code></a></a>&gt;, own&lt;<a href="#error"><a href="#error"><code>error</code></a></a>&gt;&gt;</li>
</ul>
<h4><a name="method_incoming_value.incoming_value_size"></a><code>[method]incoming-value.incoming-value-size: func</code></h4>
<p>The size of the value in bytes.
If the size is unknown or unavailable, this function returns an <code>Err(error)</code>.</p>
<h5>Params</h5>
<ul>
<li><a name="method_incoming_value.incoming_value_size.self"></a><code>self</code>: borrow&lt;<a href="#incoming_value"><a href="#incoming_value"><code>incoming-value</code></a></a>&gt;</li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="method_incoming_value.incoming_value_size.0"></a> result&lt;<code>u64</code>, own&lt;<a href="#error"><a href="#error"><code>error</code></a></a>&gt;&gt;</li>
</ul>
<h2><a name="wasi:keyvalue_eventual_0.2.0_draft"></a>Import interface wasi:keyvalue/eventual@0.2.0-draft</h2>
<p>A keyvalue interface that provides eventually consistent CRUD operations.</p>
<p>A CRUD operation is an operation that acts on a single key-value pair.</p>
<p>The value in the key-value pair is defined as a <code>u8</code> byte array and the intention
is that it is the common denominator for all data types defined by different
key-value stores to handle data, ensuring compatibility between different
key-value stores. Note: the clients will be expecting serialization/deserialization overhead
to be handled by the key-value store. The value could be a serialized object from
JSON, HTML or vendor-specific data types like AWS S3 objects.</p>
<p>Data consistency in a key value store refers to the gaurantee that once a
write operation completes, all subsequent read operations will return the
value that was written.</p>
<p>The level of consistency in readwrite interfaces is <strong>eventual consistency</strong>,
which means that if a write operation completes successfully, all subsequent
read operations will eventually return the value that was written. In other words,
if we pause the updates to the system, the system eventually will return
the last updated value for read.</p>
<hr />
<h3>Types</h3>
<h4><a name="bucket"></a><code>type bucket</code></h4>
<p><a href="#bucket"><a href="#bucket"><code>bucket</code></a></a></p>
<p>
#### <a name="error"></a>`type error`
[`error`](#error)
<p>
#### <a name="incoming_value"></a>`type incoming-value`
[`incoming-value`](#incoming_value)
<p>
#### <a name="key"></a>`type key`
[`key`](#key)
<p>
#### <a name="outgoing_value"></a>`type outgoing-value`
[`outgoing-value`](#outgoing_value)
<p>
----
<h3>Functions</h3>
<h4><a name="get"></a><code>get: func</code></h4>
<p>Get the value associated with the key in the bucket.</p>
<p>The value is returned as an option. If the key-value pair exists in the
bucket, it returns <code>Ok(value)</code>. If the key does not exist in the
bucket, it returns <code>Ok(none)</code>.</p>
<p>If any other error occurs, it returns an <code>Err(error)</code>.</p>
<h5>Params</h5>
<ul>
<li><a name="get.bucket"></a><a href="#bucket"><code>bucket</code></a>: borrow&lt;<a href="#bucket"><a href="#bucket"><code>bucket</code></a></a>&gt;</li>
<li><a name="get.key"></a><a href="#key"><code>key</code></a>: <a href="#key"><a href="#key"><code>key</code></a></a></li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="get.0"></a> result&lt;option&lt;own&lt;<a href="#incoming_value"><a href="#incoming_value"><code>incoming-value</code></a></a>&gt;&gt;, own&lt;<a href="#error"><a href="#error"><code>error</code></a></a>&gt;&gt;</li>
</ul>
<h4><a name="set"></a><code>set: func</code></h4>
<p>Set the value associated with the key in the bucket. If the key already
exists in the bucket, it overwrites the value.</p>
<p>If the key does not exist in the bucket, it creates a new key-value pair.</p>
<p>If any other error occurs, it returns an <code>Err(error)</code>.</p>
<h5>Params</h5>
<ul>
<li><a name="set.bucket"></a><a href="#bucket"><code>bucket</code></a>: borrow&lt;<a href="#bucket"><a href="#bucket"><code>bucket</code></a></a>&gt;</li>
<li><a name="set.key"></a><a href="#key"><code>key</code></a>: <a href="#key"><a href="#key"><code>key</code></a></a></li>
<li><a name="set.outgoing_value"></a><a href="#outgoing_value"><code>outgoing-value</code></a>: borrow&lt;<a href="#outgoing_value"><a href="#outgoing_value"><code>outgoing-value</code></a></a>&gt;</li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="set.0"></a> result&lt;_, own&lt;<a href="#error"><a href="#error"><code>error</code></a></a>&gt;&gt;</li>
</ul>
<h4><a name="delete"></a><code>delete: func</code></h4>
<p>Delete the key-value pair associated with the key in the bucket.</p>
<p>If the key does not exist in the bucket, it does nothing.</p>
<p>If any other error occurs, it returns an <code>Err(error)</code>.</p>
<h5>Params</h5>
<ul>
<li><a name="delete.bucket"></a><a href="#bucket"><code>bucket</code></a>: borrow&lt;<a href="#bucket"><a href="#bucket"><code>bucket</code></a></a>&gt;</li>
<li><a name="delete.key"></a><a href="#key"><code>key</code></a>: <a href="#key"><a href="#key"><code>key</code></a></a></li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="delete.0"></a> result&lt;_, own&lt;<a href="#error"><a href="#error"><code>error</code></a></a>&gt;&gt;</li>
</ul>
<h4><a name="exists"></a><code>exists: func</code></h4>
<p>Check if the key exists in the bucket.</p>
<p>If the key exists in the bucket, it returns <code>Ok(true)</code>. If the key does
not exist in the bucket, it returns <code>Ok(false)</code>.</p>
<p>If any other error occurs, it returns an <code>Err(error)</code>.</p>
<h5>Params</h5>
<ul>
<li><a name="exists.bucket"></a><a href="#bucket"><code>bucket</code></a>: borrow&lt;<a href="#bucket"><a href="#bucket"><code>bucket</code></a></a>&gt;</li>
<li><a name="exists.key"></a><a href="#key"><code>key</code></a>: <a href="#key"><a href="#key"><code>key</code></a></a></li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="exists.0"></a> result&lt;<code>bool</code>, own&lt;<a href="#error"><a href="#error"><code>error</code></a></a>&gt;&gt;</li>
</ul>
<h2><a name="wasi:keyvalue_atomic_0.2.0_draft"></a>Import interface wasi:keyvalue/atomic@0.2.0-draft</h2>
<p>A keyvalue interface that provides atomic operations.</p>
<p>Atomic operations are single, indivisible operations. When a fault causes
an atomic operation to fail, it will appear to the invoker of the atomic
operation that the action either completed successfully or did nothing
at all.</p>
<hr />
<h3>Types</h3>
<h4><a name="bucket"></a><code>type bucket</code></h4>
<p><a href="#bucket"><a href="#bucket"><code>bucket</code></a></a></p>
<p>
#### <a name="error"></a>`type error`
[`error`](#error)
<p>
#### <a name="key"></a>`type key`
[`key`](#key)
<p>
----
<h3>Functions</h3>
<h4><a name="increment"></a><code>increment: func</code></h4>
<p>Atomically increment the value associated with the key in the bucket by the
given delta. It returns the new value.</p>
<p>If the key does not exist in the bucket, it creates a new key-value pair
with the value set to the given delta.</p>
<p>If any other error occurs, it returns an <code>Err(error)</code>.</p>
<h5>Params</h5>
<ul>
<li><a name="increment.bucket"></a><a href="#bucket"><code>bucket</code></a>: borrow&lt;<a href="#bucket"><a href="#bucket"><code>bucket</code></a></a>&gt;</li>
<li><a name="increment.key"></a><a href="#key"><code>key</code></a>: <a href="#key"><a href="#key"><code>key</code></a></a></li>
<li><a name="increment.delta"></a><code>delta</code>: <code>u64</code></li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="increment.0"></a> result&lt;<code>u64</code>, own&lt;<a href="#error"><a href="#error"><code>error</code></a></a>&gt;&gt;</li>
</ul>
<h4><a name="compare_and_swap"></a><code>compare-and-swap: func</code></h4>
<p>Compare-and-swap (CAS) atomically updates the value associated with the key
in the bucket if the value matches the old value. This operation returns
<code>Ok(true)</code> if the swap was successful, <code>Ok(false)</code> if the value did not match,</p>
<p>A successful CAS operation means the current value matched the <code>old</code> value
and was replaced with the <code>new</code> value.</p>
<p>If the key does not exist in the bucket, it returns <code>Ok(false)</code>.</p>
<p>If any other error occurs, it returns an <code>Err(error)</code>.</p>
<h5>Params</h5>
<ul>
<li><a name="compare_and_swap.bucket"></a><a href="#bucket"><code>bucket</code></a>: borrow&lt;<a href="#bucket"><a href="#bucket"><code>bucket</code></a></a>&gt;</li>
<li><a name="compare_and_swap.key"></a><a href="#key"><code>key</code></a>: <a href="#key"><a href="#key"><code>key</code></a></a></li>
<li><a name="compare_and_swap.old"></a><code>old</code>: <code>u64</code></li>
<li><a name="compare_and_swap.new"></a><code>new</code>: <code>u64</code></li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="compare_and_swap.0"></a> result&lt;<code>bool</code>, own&lt;<a href="#error"><a href="#error"><code>error</code></a></a>&gt;&gt;</li>
</ul>
<h2><a name="wasi:keyvalue_eventual_batch_0.2.0_draft"></a>Import interface wasi:keyvalue/eventual-batch@0.2.0-draft</h2>
<p>A keyvalue interface that provides eventually consistent batch operations.</p>
<p>A batch operation is an operation that operates on multiple keys at once.</p>
<p>Batch operations are useful for reducing network round-trip time. For example,
if you want to get the values associated with 100 keys, you can either do 100 get
operations or you can do 1 batch get operation. The batch operation is
faster because it only needs to make 1 network call instead of 100.</p>
<p>A batch operation does not guarantee atomicity, meaning that if the batch
operation fails, some of the keys may have been modified and some may not.
Transactional operations are being worked on and will be added in the future to
provide atomicity.</p>
<p>Data consistency in a key value store refers to the gaurantee that once a
write operation completes, all subsequent read operations will return the
value that was written.</p>
<p>The level of consistency in batch operations is <strong>eventual consistency</strong>, the same
with the readwrite interface. This interface does not guarantee strong consistency,
meaning that if a write operation completes, subsequent read operations may not return
the value that was written.</p>
<hr />
<h3>Types</h3>
<h4><a name="bucket"></a><code>type bucket</code></h4>
<p><a href="#bucket"><a href="#bucket"><code>bucket</code></a></a></p>
<p>
#### <a name="error"></a>`type error`
[`error`](#error)
<p>
#### <a name="key"></a>`type key`
[`key`](#key)
<p>
#### <a name="incoming_value"></a>`type incoming-value`
[`incoming-value`](#incoming_value)
<p>
#### <a name="outgoing_value"></a>`type outgoing-value`
[`outgoing-value`](#outgoing_value)
<p>
----
<h3>Functions</h3>
<h4><a name="get_many"></a><code>get-many: func</code></h4>
<p>Get the values associated with the keys in the bucket. It returns a list of
incoming-value that can be consumed to get the value associated with the key.</p>
<p>If any of the keys do not exist in the bucket, it returns a <code>none</code> value for
that key in the list.</p>
<p>Note that the key-value pairs are guaranteed to be returned in the same order</p>
<p>MAY show an out-of-date value if there are concurrent writes to the bucket.</p>
<p>If any other error occurs, it returns an <code>Err(error)</code>.</p>
<h5>Params</h5>
<ul>
<li><a name="get_many.bucket"></a><a href="#bucket"><code>bucket</code></a>: borrow&lt;<a href="#bucket"><a href="#bucket"><code>bucket</code></a></a>&gt;</li>
<li><a name="get_many.keys"></a><a href="#keys"><code>keys</code></a>: list&lt;<a href="#key"><a href="#key"><code>key</code></a></a>&gt;</li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="get_many.0"></a> result&lt;list&lt;option&lt;own&lt;<a href="#incoming_value"><a href="#incoming_value"><code>incoming-value</code></a></a>&gt;&gt;&gt;, own&lt;<a href="#error"><a href="#error"><code>error</code></a></a>&gt;&gt;</li>
</ul>
<h4><a name="keys"></a><code>keys: func</code></h4>
<p>Get all the keys in the bucket. It returns a list of keys.</p>
<p>Note that the keys are not guaranteed to be returned in any particular order.</p>
<p>If the bucket is empty, it returns an empty list.</p>
<p>MAY show an out-of-date list of keys if there are concurrent writes to the bucket.</p>
<p>If any error occurs, it returns an <code>Err(error)</code>.</p>
<h5>Params</h5>
<ul>
<li><a name="keys.bucket"></a><a href="#bucket"><code>bucket</code></a>: borrow&lt;<a href="#bucket"><a href="#bucket"><code>bucket</code></a></a>&gt;</li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="keys.0"></a> result&lt;list&lt;<a href="#key"><a href="#key"><code>key</code></a></a>&gt;, own&lt;<a href="#error"><a href="#error"><code>error</code></a></a>&gt;&gt;</li>
</ul>
<h4><a name="set_many"></a><code>set-many: func</code></h4>
<p>Set the values associated with the keys in the bucket. If the key already
exists in the bucket, it overwrites the value.</p>
<p>Note that the key-value pairs are not guaranteed to be set in the order
they are provided.</p>
<p>If any of the keys do not exist in the bucket, it creates a new key-value pair.</p>
<p>If any other error occurs, it returns an <code>Err(error)</code>. When an error occurs, it
does not rollback the key-value pairs that were already set. Thus, this batch operation
does not guarantee atomicity, implying that some key-value pairs could be
set while others might fail.</p>
<p>Other concurrent operations may also be able to see the partial results.</p>
<h5>Params</h5>
<ul>
<li><a name="set_many.bucket"></a><a href="#bucket"><code>bucket</code></a>: borrow&lt;<a href="#bucket"><a href="#bucket"><code>bucket</code></a></a>&gt;</li>
<li><a name="set_many.key_values"></a><code>key-values</code>: list&lt;(<a href="#key"><a href="#key"><code>key</code></a></a>, borrow&lt;<a href="#outgoing_value"><a href="#outgoing_value"><code>outgoing-value</code></a></a>&gt;)&gt;</li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="set_many.0"></a> result&lt;_, own&lt;<a href="#error"><a href="#error"><code>error</code></a></a>&gt;&gt;</li>
</ul>
<h4><a name="delete_many"></a><code>delete-many: func</code></h4>
<p>Delete the key-value pairs associated with the keys in the bucket.</p>
<p>Note that the key-value pairs are not guaranteed to be deleted in the order
they are provided.</p>
<p>If any of the keys do not exist in the bucket, it skips the key.</p>
<p>If any other error occurs, it returns an <code>Err(error)</code>. When an error occurs, it
does not rollback the key-value pairs that were already deleted. Thus, this batch operation
does not guarantee atomicity, implying that some key-value pairs could be
deleted while others might fail.</p>
<p>Other concurrent operations may also be able to see the partial results.</p>
<h5>Params</h5>
<ul>
<li><a name="delete_many.bucket"></a><a href="#bucket"><code>bucket</code></a>: borrow&lt;<a href="#bucket"><a href="#bucket"><code>bucket</code></a></a>&gt;</li>
<li><a name="delete_many.keys"></a><a href="#keys"><code>keys</code></a>: list&lt;<a href="#key"><a href="#key"><code>key</code></a></a>&gt;</li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="delete_many.0"></a> result&lt;_, own&lt;<a href="#error"><a href="#error"><code>error</code></a></a>&gt;&gt;</li>
</ul>
<h2><a name="wasi:blobstore_types_0.2.0_draft"></a>Import interface wasi:blobstore/types@0.2.0-draft</h2>
<p>Types used by blobstore</p>
<hr />
<h3>Types</h3>
<h4><a name="input_stream"></a><code>type input-stream</code></h4>
<p><a href="#input_stream"><a href="#input_stream"><code>input-stream</code></a></a></p>
<p>
#### <a name="output_stream"></a>`type output-stream`
[`output-stream`](#output_stream)
<p>
#### <a name="container_name"></a>`type container-name`
`string`
<p>name of a container, a collection of objects.
The container name may be any valid UTF-8 string.
<h4><a name="object_name"></a><code>type object-name</code></h4>
<p><code>string</code></p>
<p>name of an object within a container
The object name may be any valid UTF-8 string.
<h4><a name="timestamp"></a><code>type timestamp</code></h4>
<p><code>u64</code></p>
<p>TODO: define timestamp to include seconds since
Unix epoch and nanoseconds
https://github.com/WebAssembly/wasi-blob-store/issues/7
<h4><a name="object_size"></a><code>type object-size</code></h4>
<p><code>u64</code></p>
<p>size of an object, in bytes
<h4><a name="error"></a><code>type error</code></h4>
<p><code>string</code></p>
<p>
#### <a name="container_metadata"></a>`record container-metadata`
<p>information about a container</p>
<h5>Record Fields</h5>
<ul>
<li>
<p><a name="container_metadata.name"></a><code>name</code>: <a href="#container_name"><a href="#container_name"><code>container-name</code></a></a></p>
<p>the container's name
</li>
<li>
<p><a name="container_metadata.created_at"></a><code>created-at</code>: <a href="#timestamp"><a href="#timestamp"><code>timestamp</code></a></a></p>
<p>date and time container was created
</li>
</ul>
<h4><a name="object_metadata"></a><code>record object-metadata</code></h4>
<p>information about an object</p>
<h5>Record Fields</h5>
<ul>
<li>
<p><a name="object_metadata.name"></a><code>name</code>: <a href="#object_name"><a href="#object_name"><code>object-name</code></a></a></p>
<p>the object's name
</li>
<li>
<p><a name="object_metadata.container"></a><a href="#container"><code>container</code></a>: <a href="#container_name"><a href="#container_name"><code>container-name</code></a></a></p>
<p>the object's parent container
</li>
<li>
<p><a name="object_metadata.created_at"></a><code>created-at</code>: <a href="#timestamp"><a href="#timestamp"><code>timestamp</code></a></a></p>
<p>date and time the object was created
</li>
<li>
<p><a name="object_metadata.size"></a><code>size</code>: <a href="#object_size"><a href="#object_size"><code>object-size</code></a></a></p>
<p>size of the object, in bytes
</li>
</ul>
<h4><a name="object_id"></a><code>record object-id</code></h4>
<p>identifier for an object that includes its container name</p>
<h5>Record Fields</h5>
<ul>
<li><a name="object_id.container"></a><a href="#container"><code>container</code></a>: <a href="#container_name"><a href="#container_name"><code>container-name</code></a></a></li>
<li><a name="object_id.object"></a><code>object</code>: <a href="#object_name"><a href="#object_name"><code>object-name</code></a></a></li>
</ul>
<h4><a name="outgoing_value"></a><code>resource outgoing-value</code></h4>
<p>A data is the data stored in a data blob. The value can be of any type
that can be represented in a byte array. It provides a way to write the value
to the output-stream defined in the <code>wasi-io</code> interface.
Soon: switch to <code>resource value { ... }</code></p>
<h4><a name="incoming_value"></a><code>resource incoming-value</code></h4>
<p>A incoming-value is a wrapper around a value. It provides a way to read the value
from the input-stream defined in the <code>wasi-io</code> interface.</p>
<p>The incoming-value provides two ways to consume the value:</p>
<ol>
<li><code>incoming-value-consume-sync</code> consumes the value synchronously and returns the
value as a list of bytes.</li>
<li><code>incoming-value-consume-async</code> consumes the value asynchronously and returns the
value as an input-stream.
Soon: switch to <code>resource incoming-value { ... }</code></li>
</ol>
<h4><a name="incoming_value_async_body"></a><code>type incoming-value-async-body</code></h4>
<p><a href="#input_stream"><a href="#input_stream"><code>input-stream</code></a></a></p>
<p>
#### <a name="incoming_value_sync_body"></a>`type incoming-value-sync-body`
[`incoming-value-sync-body`](#incoming_value_sync_body)
<p>
----
<h3>Functions</h3>
<h4><a name="static_outgoing_value.new_outgoing_value"></a><code>[static]outgoing-value.new-outgoing-value: func</code></h4>
<h5>Return values</h5>
<ul>
<li><a name="static_outgoing_value.new_outgoing_value.0"></a> own&lt;<a href="#outgoing_value"><a href="#outgoing_value"><code>outgoing-value</code></a></a>&gt;</li>
</ul>
<h4><a name="method_outgoing_value.outgoing_value_write_body"></a><code>[method]outgoing-value.outgoing-value-write-body: func</code></h4>
<h5>Params</h5>
<ul>
<li><a name="method_outgoing_value.outgoing_value_write_body.self"></a><code>self</code>: borrow&lt;<a href="#outgoing_value"><a href="#outgoing_value"><code>outgoing-value</code></a></a>&gt;</li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="method_outgoing_value.outgoing_value_write_body.0"></a> result&lt;own&lt;<a href="#output_stream"><a href="#output_stream"><code>output-stream</code></a></a>&gt;&gt;</li>
</ul>
<h4><a name="method_incoming_value.incoming_value_consume_sync"></a><code>[method]incoming-value.incoming-value-consume-sync: func</code></h4>
<h5>Params</h5>
<ul>
<li><a name="method_incoming_value.incoming_value_consume_sync.self"></a><code>self</code>: borrow&lt;<a href="#incoming_value"><a href="#incoming_value"><code>incoming-value</code></a></a>&gt;</li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="method_incoming_value.incoming_value_consume_sync.0"></a> result&lt;<a href="#incoming_value_sync_body"><a href="#incoming_value_sync_body"><code>incoming-value-sync-body</code></a></a>, <a href="#error"><a href="#error"><code>error</code></a></a>&gt;</li>
</ul>
<h4><a name="method_incoming_value.incoming_value_consume_async"></a><code>[method]incoming-value.incoming-value-consume-async: func</code></h4>
<h5>Params</h5>
<ul>
<li><a name="method_incoming_value.incoming_value_consume_async.self"></a><code>self</code>: borrow&lt;<a href="#incoming_value"><a href="#incoming_value"><code>incoming-value</code></a></a>&gt;</li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="method_incoming_value.incoming_value_consume_async.0"></a> result&lt;own&lt;<a href="#incoming_value_async_body"><a href="#incoming_value_async_body"><code>incoming-value-async-body</code></a></a>&gt;, <a href="#error"><a href="#error"><code>error</code></a></a>&gt;</li>
</ul>
<h4><a name="method_incoming_value.size"></a><code>[method]incoming-value.size: func</code></h4>
<h5>Params</h5>
<ul>
<li><a name="method_incoming_value.size.self"></a><code>self</code>: borrow&lt;<a href="#incoming_value"><a href="#incoming_value"><code>incoming-value</code></a></a>&gt;</li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="method_incoming_value.size.0"></a> <code>u64</code></li>
</ul>
<h2><a name="wasi:blobstore_container_0.2.0_draft"></a>Import interface wasi:blobstore/container@0.2.0-draft</h2>
<p>a Container is a collection of objects</p>
<hr />
<h3>Types</h3>
<h4><a name="input_stream"></a><code>type input-stream</code></h4>
<p><a href="#input_stream"><a href="#input_stream"><code>input-stream</code></a></a></p>
<p>
#### <a name="output_stream"></a>`type output-stream`
[`output-stream`](#output_stream)
<p>
#### <a name="container_metadata"></a>`type container-metadata`
[`container-metadata`](#container_metadata)
<p>
#### <a name="error"></a>`type error`
[`error`](#error)
<p>
#### <a name="incoming_value"></a>`type incoming-value`
[`incoming-value`](#incoming_value)
<p>
#### <a name="object_metadata"></a>`type object-metadata`
[`object-metadata`](#object_metadata)
<p>
#### <a name="object_name"></a>`type object-name`
[`object-name`](#object_name)
<p>
#### <a name="outgoing_value"></a>`type outgoing-value`
[`outgoing-value`](#outgoing_value)
<p>
#### <a name="container"></a>`resource container`
<p>this defines the <a href="#container"><code>container</code></a> resource</p>
<h4><a name="stream_object_names"></a><code>resource stream-object-names</code></h4>
<h2>this defines the <a href="#stream_object_names"><code>stream-object-names</code></a> resource which is a representation of stream<object-name></h2>
<h3>Functions</h3>
<h4><a name="method_container.name"></a><code>[method]container.name: func</code></h4>
<p>returns container name</p>
<h5>Params</h5>
<ul>
<li><a name="method_container.name.self"></a><code>self</code>: borrow&lt;<a href="#container"><a href="#container"><code>container</code></a></a>&gt;</li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="method_container.name.0"></a> result&lt;<code>string</code>, <a href="#error"><a href="#error"><code>error</code></a></a>&gt;</li>
</ul>
<h4><a name="method_container.info"></a><code>[method]container.info: func</code></h4>
<p>returns container metadata</p>
<h5>Params</h5>
<ul>
<li><a name="method_container.info.self"></a><code>self</code>: borrow&lt;<a href="#container"><a href="#container"><code>container</code></a></a>&gt;</li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="method_container.info.0"></a> result&lt;<a href="#container_metadata"><a href="#container_metadata"><code>container-metadata</code></a></a>, <a href="#error"><a href="#error"><code>error</code></a></a>&gt;</li>
</ul>
<h4><a name="method_container.get_data"></a><code>[method]container.get-data: func</code></h4>
<p>retrieves an object or portion of an object, as a resource.
Start and end offsets are inclusive.
Once a data-blob resource has been created, the underlying bytes are held by the blobstore service for the lifetime
of the data-blob resource, even if the object they came from is later deleted.</p>
<h5>Params</h5>
<ul>
<li><a name="method_container.get_data.self"></a><code>self</code>: borrow&lt;<a href="#container"><a href="#container"><code>container</code></a></a>&gt;</li>
<li><a name="method_container.get_data.name"></a><code>name</code>: <a href="#object_name"><a href="#object_name"><code>object-name</code></a></a></li>
<li><a name="method_container.get_data.start"></a><code>start</code>: <code>u64</code></li>
<li><a name="method_container.get_data.end"></a><code>end</code>: <code>u64</code></li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="method_container.get_data.0"></a> result&lt;own&lt;<a href="#incoming_value"><a href="#incoming_value"><code>incoming-value</code></a></a>&gt;, <a href="#error"><a href="#error"><code>error</code></a></a>&gt;</li>
</ul>
<h4><a name="method_container.write_data"></a><code>[method]container.write-data: func</code></h4>
<p>creates or replaces an object with the data blob.</p>
<h5>Params</h5>
<ul>
<li><a name="method_container.write_data.self"></a><code>self</code>: borrow&lt;<a href="#container"><a href="#container"><code>container</code></a></a>&gt;</li>
<li><a name="method_container.write_data.name"></a><code>name</code>: <a href="#object_name"><a href="#object_name"><code>object-name</code></a></a></li>
<li><a name="method_container.write_data.data"></a><code>data</code>: borrow&lt;<a href="#outgoing_value"><a href="#outgoing_value"><code>outgoing-value</code></a></a>&gt;</li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="method_container.write_data.0"></a> result&lt;_, <a href="#error"><a href="#error"><code>error</code></a></a>&gt;</li>
</ul>
<h4><a name="method_container.list_objects"></a><code>[method]container.list-objects: func</code></h4>
<p>returns list of objects in the container. Order is undefined.</p>
<h5>Params</h5>
<ul>
<li><a name="method_container.list_objects.self"></a><code>self</code>: borrow&lt;<a href="#container"><a href="#container"><code>container</code></a></a>&gt;</li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="method_container.list_objects.0"></a> result&lt;own&lt;<a href="#stream_object_names"><a href="#stream_object_names"><code>stream-object-names</code></a></a>&gt;, <a href="#error"><a href="#error"><code>error</code></a></a>&gt;</li>
</ul>
<h4><a name="method_container.delete_object"></a><code>[method]container.delete-object: func</code></h4>
<p>deletes object.
does not return error if object did not exist.</p>
<h5>Params</h5>
<ul>
<li><a name="method_container.delete_object.self"></a><code>self</code>: borrow&lt;<a href="#container"><a href="#container"><code>container</code></a></a>&gt;</li>
<li><a name="method_container.delete_object.name"></a><code>name</code>: <a href="#object_name"><a href="#object_name"><code>object-name</code></a></a></li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="method_container.delete_object.0"></a> result&lt;_, <a href="#error"><a href="#error"><code>error</code></a></a>&gt;</li>
</ul>
<h4><a name="method_container.delete_objects"></a><code>[method]container.delete-objects: func</code></h4>
<p>deletes multiple objects in the container</p>
<h5>Params</h5>
<ul>
<li><a name="method_container.delete_objects.self"></a><code>self</code>: borrow&lt;<a href="#container"><a href="#container"><code>container</code></a></a>&gt;</li>
<li><a name="method_container.delete_objects.names"></a><code>names</code>: list&lt;<a href="#object_name"><a href="#object_name"><code>object-name</code></a></a>&gt;</li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="method_container.delete_objects.0"></a> result&lt;_, <a href="#error"><a href="#error"><code>error</code></a></a>&gt;</li>
</ul>
<h4><a name="method_container.has_object"></a><code>[method]container.has-object: func</code></h4>
<p>returns true if the object exists in this container</p>
<h5>Params</h5>
<ul>
<li><a name="method_container.has_object.self"></a><code>self</code>: borrow&lt;<a href="#container"><a href="#container"><code>container</code></a></a>&gt;</li>
<li><a name="method_container.has_object.name"></a><code>name</code>: <a href="#object_name"><a href="#object_name"><code>object-name</code></a></a></li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="method_container.has_object.0"></a> result&lt;<code>bool</code>, <a href="#error"><a href="#error"><code>error</code></a></a>&gt;</li>
</ul>
<h4><a name="method_container.object_info"></a><code>[method]container.object-info: func</code></h4>
<p>returns metadata for the object</p>
<h5>Params</h5>
<ul>
<li><a name="method_container.object_info.self"></a><code>self</code>: borrow&lt;<a href="#container"><a href="#container"><code>container</code></a></a>&gt;</li>
<li><a name="method_container.object_info.name"></a><code>name</code>: <a href="#object_name"><a href="#object_name"><code>object-name</code></a></a></li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="method_container.object_info.0"></a> result&lt;<a href="#object_metadata"><a href="#object_metadata"><code>object-metadata</code></a></a>, <a href="#error"><a href="#error"><code>error</code></a></a>&gt;</li>
</ul>
<h4><a name="method_container.clear"></a><code>[method]container.clear: func</code></h4>
<p>removes all objects within the container, leaving the container empty.</p>
<h5>Params</h5>
<ul>
<li><a name="method_container.clear.self"></a><code>self</code>: borrow&lt;<a href="#container"><a href="#container"><code>container</code></a></a>&gt;</li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="method_container.clear.0"></a> result&lt;_, <a href="#error"><a href="#error"><code>error</code></a></a>&gt;</li>
</ul>
<h4><a name="method_stream_object_names.read_stream_object_names"></a><code>[method]stream-object-names.read-stream-object-names: func</code></h4>
<p>reads the next number of objects from the stream</p>
<p>This function returns the list of objects read, and a boolean indicating if the end of the stream was reached.</p>
<h5>Params</h5>
<ul>
<li><a name="method_stream_object_names.read_stream_object_names.self"></a><code>self</code>: borrow&lt;<a href="#stream_object_names"><a href="#stream_object_names"><code>stream-object-names</code></a></a>&gt;</li>
<li><a name="method_stream_object_names.read_stream_object_names.len"></a><code>len</code>: <code>u64</code></li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="method_stream_object_names.read_stream_object_names.0"></a> result&lt;(list&lt;<a href="#object_name"><a href="#object_name"><code>object-name</code></a></a>&gt;, <code>bool</code>), <a href="#error"><a href="#error"><code>error</code></a></a>&gt;</li>
</ul>
<h4><a name="method_stream_object_names.skip_stream_object_names"></a><code>[method]stream-object-names.skip-stream-object-names: func</code></h4>
<p>skip the next number of objects in the stream</p>
<p>This function returns the number of objects skipped, and a boolean indicating if the end of the stream was reached.</p>
<h5>Params</h5>
<ul>
<li><a name="method_stream_object_names.skip_stream_object_names.self"></a><code>self</code>: borrow&lt;<a href="#stream_object_names"><a href="#stream_object_names"><code>stream-object-names</code></a></a>&gt;</li>
<li><a name="method_stream_object_names.skip_stream_object_names.num"></a><code>num</code>: <code>u64</code></li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="method_stream_object_names.skip_stream_object_names.0"></a> result&lt;(<code>u64</code>, <code>bool</code>), <a href="#error"><a href="#error"><code>error</code></a></a>&gt;</li>
</ul>
<h2><a name="wasi:blobstore_blobstore_0.2.0_draft"></a>Import interface wasi:blobstore/blobstore@0.2.0-draft</h2>
<p>wasi-cloud Blobstore service definition</p>
<hr />
<h3>Types</h3>
<h4><a name="container"></a><code>type container</code></h4>
<p><a href="#container"><a href="#container"><code>container</code></a></a></p>
<p>
#### <a name="error"></a>`type error`
[`error`](#error)
<p>
#### <a name="container_name"></a>`type container-name`
[`container-name`](#container_name)
<p>
#### <a name="object_id"></a>`type object-id`
[`object-id`](#object_id)
<p>
----
<h3>Functions</h3>
<h4><a name="create_container"></a><code>create-container: func</code></h4>
<p>creates a new empty container</p>
<h5>Params</h5>
<ul>
<li><a name="create_container.name"></a><code>name</code>: <a href="#container_name"><a href="#container_name"><code>container-name</code></a></a></li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="create_container.0"></a> result&lt;own&lt;<a href="#container"><a href="#container"><code>container</code></a></a>&gt;, <a href="#error"><a href="#error"><code>error</code></a></a>&gt;</li>
</ul>
<h4><a name="get_container"></a><code>get-container: func</code></h4>
<p>retrieves a container by name</p>
<h5>Params</h5>
<ul>
<li><a name="get_container.name"></a><code>name</code>: <a href="#container_name"><a href="#container_name"><code>container-name</code></a></a></li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="get_container.0"></a> result&lt;own&lt;<a href="#container"><a href="#container"><code>container</code></a></a>&gt;, <a href="#error"><a href="#error"><code>error</code></a></a>&gt;</li>
</ul>
<h4><a name="delete_container"></a><code>delete-container: func</code></h4>
<p>deletes a container and all objects within it</p>
<h5>Params</h5>
<ul>
<li><a name="delete_container.name"></a><code>name</code>: <a href="#container_name"><a href="#container_name"><code>container-name</code></a></a></li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="delete_container.0"></a> result&lt;_, <a href="#error"><a href="#error"><code>error</code></a></a>&gt;</li>
</ul>
<h4><a name="container_exists"></a><code>container-exists: func</code></h4>
<p>returns true if the container exists</p>
<h5>Params</h5>
<ul>
<li><a name="container_exists.name"></a><code>name</code>: <a href="#container_name"><a href="#container_name"><code>container-name</code></a></a></li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="container_exists.0"></a> result&lt;<code>bool</code>, <a href="#error"><a href="#error"><code>error</code></a></a>&gt;</li>
</ul>
<h4><a name="copy_object"></a><code>copy-object: func</code></h4>
<p>copies (duplicates) an object, to the same or a different container.
returns an error if the target container does not exist.
overwrites destination object if it already existed.</p>
<h5>Params</h5>
<ul>
<li><a name="copy_object.src"></a><code>src</code>: <a href="#object_id"><a href="#object_id"><code>object-id</code></a></a></li>
<li><a name="copy_object.dest"></a><code>dest</code>: <a href="#object_id"><a href="#object_id"><code>object-id</code></a></a></li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="copy_object.0"></a> result&lt;_, <a href="#error"><a href="#error"><code>error</code></a></a>&gt;</li>
</ul>
<h4><a name="move_object"></a><code>move-object: func</code></h4>
<p>moves or renames an object, to the same or a different container
returns an error if the destination container does not exist.
overwrites destination object if it already existed.</p>
<h5>Params</h5>
<ul>
<li><a name="move_object.src"></a><code>src</code>: <a href="#object_id"><a href="#object_id"><code>object-id</code></a></a></li>
<li><a name="move_object.dest"></a><code>dest</code>: <a href="#object_id"><a href="#object_id"><code>object-id</code></a></a></li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="move_object.0"></a> result&lt;_, <a href="#error"><a href="#error"><code>error</code></a></a>&gt;</li>
</ul>
<h2><a name="wasi:messaging_messaging_types_0.2.0_draft"></a>Import interface wasi:messaging/messaging-types@0.2.0-draft</h2>
<hr />
<h3>Types</h3>
<h4><a name="client"></a><code>resource client</code></h4>
<p>A connection to a message-exchange service (e.g., buffer, broker, etc.).</p>
<h4><a name="error"></a><code>resource error</code></h4>
<p>TODO(danbugs): This should be eventually extracted as an underlying type for other wasi-cloud-core interfaces.</p>
<h4><a name="channel"></a><code>type channel</code></h4>
<p><code>string</code></p>
<p>There are two types of channels:
- publish-subscribe channel, which is a broadcast channel, and
- point-to-point channel, which is a unicast channel.
<p>The interface doesn't highlight this difference in the type itself as that's uniquely a consumer issue.</p>
<h4><a name="guest_configuration"></a><code>record guest-configuration</code></h4>
<p>Configuration includes a required list of channels the guest is subscribing to, and an optional list of extensions key-value pairs
(e.g., partitions/offsets to read from in Kafka/EventHubs, QoS etc.).</p>
<h5>Record Fields</h5>
<ul>
<li><a name="guest_configuration.channels"></a><code>channels</code>: list&lt;<a href="#channel"><a href="#channel"><code>channel</code></a></a>&gt;</li>
<li><a name="guest_configuration.extensions"></a><code>extensions</code>: option&lt;list&lt;(<code>string</code>, <code>string</code>)&gt;&gt;</li>
</ul>
<h4><a name="format_spec"></a><code>enum format-spec</code></h4>
<p>Format specification for messages</p>
<ul>
<li>more info: https://github.com/clemensv/spec/blob/registry-extensions/registry/spec.md#message-formats</li>
<li>message metadata can further decorate w/ things like format version, and so on.</li>
</ul>
<h5>Enum Cases</h5>
<ul>
<li><a name="format_spec.cloudevents"></a><code>cloudevents</code></li>
<li><a name="format_spec.http"></a><code>http</code></li>
<li><a name="format_spec.amqp"></a><code>amqp</code></li>
<li><a name="format_spec.mqtt"></a><code>mqtt</code></li>
<li><a name="format_spec.kafka"></a><code>kafka</code></li>
<li><a name="format_spec.raw"></a><code>raw</code></li>
</ul>
<h4><a name="message"></a><code>record message</code></h4>
<p>A message with a binary payload, a format specification, and decorative metadata.</p>
<h5>Record Fields</h5>
<ul>
<li><a name="message.data"></a><code>data</code>: list&lt;<code>u8</code>&gt;</li>
<li><a name="message.format"></a><code>format</code>: <a href="#format_spec"><a href="#format_spec"><code>format-spec</code></a></a></li>
<li><a name="message.metadata"></a><code>metadata</code>: option&lt;list&lt;(<code>string</code>, <code>string</code>)&gt;&gt;</li>
</ul>
<hr />
<h3>Functions</h3>
<h4><a name="static_client.connect"></a><code>[static]client.connect: func</code></h4>
<h5>Params</h5>
<ul>
<li><a name="static_client.connect.name"></a><code>name</code>: <code>string</code></li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="static_client.connect.0"></a> result&lt;own&lt;<a href="#client"><a href="#client"><code>client</code></a></a>&gt;, own&lt;<a href="#error"><a href="#error"><code>error</code></a></a>&gt;&gt;</li>
</ul>
<h4><a name="static_error.trace"></a><code>[static]error.trace: func</code></h4>
<h5>Return values</h5>
<ul>
<li><a name="static_error.trace.0"></a> <code>string</code></li>
</ul>
<h2><a name="wasi:messaging_producer_0.2.0_draft"></a>Import interface wasi:messaging/producer@0.2.0-draft</h2>
<hr />
<h3>Types</h3>
<h4><a name="client"></a><code>type client</code></h4>
<p><a href="#client"><a href="#client"><code>client</code></a></a></p>
<p>
#### <a name="channel"></a>`type channel`
[`channel`](#channel)
<p>
#### <a name="message"></a>`type message`
[`message`](#message)
<p>
#### <a name="error"></a>`type error`
[`error`](#error)
<p>
----
<h3>Functions</h3>
<h4><a name="send"></a><code>send: func</code></h4>
<h5>Params</h5>
<ul>
<li><a name="send.c"></a><code>c</code>: own&lt;<a href="#client"><a href="#client"><code>client</code></a></a>&gt;</li>
<li><a name="send.ch"></a><code>ch</code>: <a href="#channel"><a href="#channel"><code>channel</code></a></a></li>
<li><a name="send.m"></a><code>m</code>: list&lt;<a href="#message"><a href="#message"><code>message</code></a></a>&gt;</li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="send.0"></a> result&lt;_, own&lt;<a href="#error"><a href="#error"><code>error</code></a></a>&gt;&gt;</li>
</ul>
<h2><a name="wasi:messaging_consumer_0.2.0_draft"></a>Import interface wasi:messaging/consumer@0.2.0-draft</h2>
<hr />
<h3>Types</h3>
<h4><a name="client"></a><code>type client</code></h4>
<p><a href="#client"><a href="#client"><code>client</code></a></a></p>
<p>
#### <a name="message"></a>`type message`
[`message`](#message)
<p>
#### <a name="channel"></a>`type channel`
[`channel`](#channel)
<p>
#### <a name="error"></a>`type error`
[`error`](#error)
<p>
#### <a name="guest_configuration"></a>`type guest-configuration`
[`guest-configuration`](#guest_configuration)
<p>
----
<h3>Functions</h3>
<h4><a name="subscribe_try_receive"></a><code>subscribe-try-receive: func</code></h4>
<p>Blocking receive for t-milliseconds with ephemeral subscription – if no message is received, returns None</p>
<h5>Params</h5>
<ul>
<li><a name="subscribe_try_receive.c"></a><code>c</code>: own&lt;<a href="#client"><a href="#client"><code>client</code></a></a>&gt;</li>
<li><a name="subscribe_try_receive.ch"></a><code>ch</code>: <a href="#channel"><a href="#channel"><code>channel</code></a></a></li>
<li><a name="subscribe_try_receive.t_milliseconds"></a><code>t-milliseconds</code>: <code>u32</code></li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="subscribe_try_receive.0"></a> result&lt;option&lt;list&lt;<a href="#message"><a href="#message"><code>message</code></a></a>&gt;&gt;, own&lt;<a href="#error"><a href="#error"><code>error</code></a></a>&gt;&gt;</li>
</ul>
<h4><a name="subscribe_receive"></a><code>subscribe-receive: func</code></h4>
<p>Blocking receive until message with ephemeral subscription</p>
<h5>Params</h5>
<ul>
<li><a name="subscribe_receive.c"></a><code>c</code>: own&lt;<a href="#client"><a href="#client"><code>client</code></a></a>&gt;</li>
<li><a name="subscribe_receive.ch"></a><code>ch</code>: <a href="#channel"><a href="#channel"><code>channel</code></a></a></li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="subscribe_receive.0"></a> result&lt;list&lt;<a href="#message"><a href="#message"><code>message</code></a></a>&gt;, own&lt;<a href="#error"><a href="#error"><code>error</code></a></a>&gt;&gt;</li>
</ul>
<h4><a name="update_guest_configuration"></a><code>update-guest-configuration: func</code></h4>
<p>'Fit-all' type function for updating a guest's configuration – this could be useful for:</p>
<ul>
<li>unsubscribing from a channel,</li>
<li>checkpointing,</li>
<li>etc..</li>
</ul>
<h5>Params</h5>
<ul>
<li><a name="update_guest_configuration.gc"></a><code>gc</code>: <a href="#guest_configuration"><a href="#guest_configuration"><code>guest-configuration</code></a></a></li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="update_guest_configuration.0"></a> result&lt;_, own&lt;<a href="#error"><a href="#error"><code>error</code></a></a>&gt;&gt;</li>
</ul>
<h4><a name="complete_message"></a><code>complete-message: func</code></h4>
<p>A message can exist under several statuses:
(1) available: the message is ready to be read,
(2) acquired: the message has been sent to a consumer (but still exists in the queue),
(3) accepted (result of complete-message): the message has been received and ACK-ed by a consumer and can be safely removed from the queue,
(4) rejected (result of abandon-message): the message has been received and NACK-ed by a consumer, at which point it can be:</p>
<ul>
<li>deleted,</li>
<li>sent to a dead-letter queue, or</li>
<li>kept in the queue for further processing.</li>
</ul>
<h5>Params</h5>
<ul>
<li><a name="complete_message.m"></a><code>m</code>: <a href="#message"><a href="#message"><code>message</code></a></a></li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="complete_message.0"></a> result&lt;_, own&lt;<a href="#error"><a href="#error"><code>error</code></a></a>&gt;&gt;</li>
</ul>
<h4><a name="abandon_message"></a><code>abandon-message: func</code></h4>
<h5>Params</h5>
<ul>
<li><a name="abandon_message.m"></a><code>m</code>: <a href="#message"><a href="#message"><code>message</code></a></a></li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="abandon_message.0"></a> result&lt;_, own&lt;<a href="#error"><a href="#error"><code>error</code></a></a>&gt;&gt;</li>
</ul>
<h2><a name="wasi:sql_types_0.2.0_draft"></a>Import interface wasi:sql/types@0.2.0-draft</h2>
<hr />
<h3>Types</h3>
<h4><a name="data_type"></a><code>variant data-type</code></h4>
<p>common data types</p>
<h5>Variant Cases</h5>
<ul>
<li><a name="data_type.int32"></a><code>int32</code>: <code>s32</code></li>
<li><a name="data_type.int64"></a><code>int64</code>: <code>s64</code></li>
<li><a name="data_type.uint32"></a><code>uint32</code>: <code>u32</code></li>
<li><a name="data_type.uint64"></a><code>uint64</code>: <code>u64</code></li>
<li><a name="data_type.float"></a><code>float</code>: <code>float64</code></li>
<li><a name="data_type.double"></a><code>double</code>: <code>float64</code></li>
<li><a name="data_type.str"></a><code>str</code>: <code>string</code></li>
<li><a name="data_type.boolean"></a><code>boolean</code>: <code>bool</code></li>
<li><a name="data_type.date"></a><code>date</code>: <code>string</code></li>
<li><a name="data_type.time"></a><code>time</code>: <code>string</code></li>
<li><a name="data_type.timestamp"></a><a href="#timestamp"><code>timestamp</code></a>: <code>string</code></li>
<li><a name="data_type.binary"></a><code>binary</code>: list&lt;<code>u8</code>&gt;</li>
<li><a name="data_type.null"></a><code>null</code></li>
</ul>
<h4><a name="row"></a><code>record row</code></h4>
<p>one single row item</p>
<h5>Record Fields</h5>
<ul>
<li><a name="row.field_name"></a><code>field-name</code>: <code>string</code></li>
<li><a name="row.value"></a><code>value</code>: <a href="#data_type"><a href="#data_type"><code>data-type</code></a></a></li>
</ul>
<h4><a name="statement"></a><code>resource statement</code></h4>
<p>allows parameterized queries
e.g., prepare(&quot;SELECT * FROM users WHERE name = ? AND age = ?&quot;, vec![&quot;John Doe&quot;, &quot;32&quot;])</p>
<h4><a name="error"></a><code>resource error</code></h4>
<p>An error resource type.
Currently, this provides only one function to return a string representation
of the error. In the future, this will be extended to provide more information.</p>
<h4><a name="connection"></a><code>resource connection</code></h4>
<h2>A connection to a sql store.</h2>
<h3>Functions</h3>
<h4><a name="static_statement.prepare"></a><code>[static]statement.prepare: func</code></h4>
<h5>Params</h5>
<ul>
<li><a name="static_statement.prepare.query"></a><a href="#query"><code>query</code></a>: <code>string</code></li>
<li><a name="static_statement.prepare.params"></a><code>params</code>: list&lt;<code>string</code>&gt;</li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="static_statement.prepare.0"></a> result&lt;own&lt;<a href="#statement"><a href="#statement"><code>statement</code></a></a>&gt;, own&lt;<a href="#error"><a href="#error"><code>error</code></a></a>&gt;&gt;</li>
</ul>
<h4><a name="method_error.trace"></a><code>[method]error.trace: func</code></h4>
<h5>Params</h5>
<ul>
<li><a name="method_error.trace.self"></a><code>self</code>: borrow&lt;<a href="#error"><a href="#error"><code>error</code></a></a>&gt;</li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="method_error.trace.0"></a> <code>string</code></li>
</ul>
<h4><a name="static_connection.open"></a><code>[static]connection.open: func</code></h4>
<h5>Params</h5>
<ul>
<li><a name="static_connection.open.name"></a><code>name</code>: <code>string</code></li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="static_connection.open.0"></a> result&lt;own&lt;<a href="#connection"><a href="#connection"><code>connection</code></a></a>&gt;, own&lt;<a href="#error"><a href="#error"><code>error</code></a></a>&gt;&gt;</li>
</ul>
<h2><a name="wasi:sql_readwrite_0.2.0_draft"></a>Import interface wasi:sql/readwrite@0.2.0-draft</h2>
<hr />
<h3>Types</h3>
<h4><a name="statement"></a><code>type statement</code></h4>
<p><a href="#statement"><a href="#statement"><code>statement</code></a></a></p>
<p>
#### <a name="row"></a>`type row`
[`row`](#row)
<p>
#### <a name="error"></a>`type error`
[`error`](#error)
<p>
#### <a name="connection"></a>`type connection`
[`connection`](#connection)
<p>
----
<h3>Functions</h3>
<h4><a name="query"></a><code>query: func</code></h4>
<p>query is optimized for querying data, and
implementors can make use of that fact to optimize
the performance of query execution (e.g., using
indexes).</p>
<h5>Params</h5>
<ul>
<li><a name="query.c"></a><code>c</code>: borrow&lt;<a href="#connection"><a href="#connection"><code>connection</code></a></a>&gt;</li>
<li><a name="query.q"></a><code>q</code>: borrow&lt;<a href="#statement"><a href="#statement"><code>statement</code></a></a>&gt;</li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="query.0"></a> result&lt;list&lt;<a href="#row"><a href="#row"><code>row</code></a></a>&gt;, own&lt;<a href="#error"><a href="#error"><code>error</code></a></a>&gt;&gt;</li>
</ul>
<h4><a name="exec"></a><code>exec: func</code></h4>
<p>exec is for modifying data in the database.</p>
<h5>Params</h5>
<ul>
<li><a name="exec.c"></a><code>c</code>: borrow&lt;<a href="#connection"><a href="#connection"><code>connection</code></a></a>&gt;</li>
<li><a name="exec.q"></a><code>q</code>: borrow&lt;<a href="#statement"><a href="#statement"><code>statement</code></a></a>&gt;</li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="exec.0"></a> result&lt;<code>u32</code>, own&lt;<a href="#error"><a href="#error"><code>error</code></a></a>&gt;&gt;</li>
</ul>
<h2><a name="wasi:config_runtime_0.2.0_draft"></a>Import interface wasi:config/runtime@0.2.0-draft</h2>
<hr />
<h3>Types</h3>
<h4><a name="config_error"></a><code>variant config-error</code></h4>
<p>An error type that encapsulates the different errors that can occur fetching config</p>
<h5>Variant Cases</h5>
<ul>
<li>
<p><a name="config_error.upstream"></a><code>upstream</code>: <code>string</code></p>
<p>This indicates an error from an "upstream" config source.
As this could be almost _anything_ (such as Vault, Kubernetes ConfigMaps, KeyValue buckets, etc),
the error message is a string.
</li>
<li>
<p><a name="config_error.io"></a><code>io</code>: <code>string</code></p>
<p>This indicates an error from an I/O operation.
As this could be almost _anything_ (such as a file read, network connection, etc),
the error message is a string.
Depending on how this ends up being consumed,
we may consider moving this to use the `wasi:io/error` type instead.
For simplicity right now in supporting multiple implementations, it is being left as a string.
</li>
</ul>
<hr />
<h3>Functions</h3>
<h4><a name="get"></a><code>get: func</code></h4>
<p>Gets a single opaque config value set at the given key if it exists</p>
<h5>Params</h5>
<ul>
<li><a name="get.key"></a><a href="#key"><code>key</code></a>: <code>string</code></li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="get.0"></a> result&lt;option&lt;list&lt;<code>u8</code>&gt;&gt;, <a href="#config_error"><a href="#config_error"><code>config-error</code></a></a>&gt;</li>
</ul>
<h4><a name="get_all"></a><code>get-all: func</code></h4>
<p>Gets a list of all set config data</p>
<h5>Return values</h5>
<ul>
<li><a name="get_all.0"></a> result&lt;list&lt;(<code>string</code>, list&lt;<code>u8</code>&gt;)&gt;, <a href="#config_error"><a href="#config_error"><code>config-error</code></a></a>&gt;</li>
</ul>
<h2><a name="wasi:random_random_0.2.0"></a>Import interface wasi:random/random@0.2.0</h2>
<p>WASI Random is a random data API.</p>
<p>It is intended to be portable at least between Unix-family platforms and
Windows.</p>
<hr />
<h3>Functions</h3>
<h4><a name="get_random_bytes"></a><code>get-random-bytes: func</code></h4>
<p>Return <code>len</code> cryptographically-secure random or pseudo-random bytes.</p>
<p>This function must produce data at least as cryptographically secure and
fast as an adequately seeded cryptographically-secure pseudo-random
number generator (CSPRNG). It must not block, from the perspective of
the calling program, under any circumstances, including on the first
request and on requests for numbers of bytes. The returned data must
always be unpredictable.</p>
<p>This function must always return fresh data. Deterministic environments
must omit this function, rather than implementing it with deterministic
data.</p>
<h5>Params</h5>
<ul>
<li><a name="get_random_bytes.len"></a><code>len</code>: <code>u64</code></li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="get_random_bytes.0"></a> list&lt;<code>u8</code>&gt;</li>
</ul>
<h4><a name="get_random_u64"></a><code>get-random-u64: func</code></h4>
<p>Return a cryptographically-secure random or pseudo-random <code>u64</code> value.</p>
<p>This function returns the same type of data as <a href="#get_random_bytes"><code>get-random-bytes</code></a>,
represented as a <code>u64</code>.</p>
<h5>Return values</h5>
<ul>
<li><a name="get_random_u64.0"></a> <code>u64</code></li>
</ul>
<h2><a name="wasi:cli_stdout_0.2.0"></a>Import interface wasi:cli/stdout@0.2.0</h2>
<hr />
<h3>Types</h3>
<h4><a name="output_stream"></a><code>type output-stream</code></h4>
<p><a href="#output_stream"><a href="#output_stream"><code>output-stream</code></a></a></p>
<p>
----
<h3>Functions</h3>
<h4><a name="get_stdout"></a><code>get-stdout: func</code></h4>
<h5>Return values</h5>
<ul>
<li><a name="get_stdout.0"></a> own&lt;<a href="#output_stream"><a href="#output_stream"><code>output-stream</code></a></a>&gt;</li>
</ul>
<h2><a name="wasi:cli_stderr_0.2.0"></a>Import interface wasi:cli/stderr@0.2.0</h2>
<hr />
<h3>Types</h3>
<h4><a name="output_stream"></a><code>type output-stream</code></h4>
<p><a href="#output_stream"><a href="#output_stream"><code>output-stream</code></a></a></p>
<p>
----
<h3>Functions</h3>
<h4><a name="get_stderr"></a><code>get-stderr: func</code></h4>
<h5>Return values</h5>
<ul>
<li><a name="get_stderr.0"></a> own&lt;<a href="#output_stream"><a href="#output_stream"><code>output-stream</code></a></a>&gt;</li>
</ul>
<h2><a name="wasi:cli_stdin_0.2.0"></a>Import interface wasi:cli/stdin@0.2.0</h2>
<hr />
<h3>Types</h3>
<h4><a name="input_stream"></a><code>type input-stream</code></h4>
<p><a href="#input_stream"><a href="#input_stream"><code>input-stream</code></a></a></p>
<p>
----
<h3>Functions</h3>
<h4><a name="get_stdin"></a><code>get-stdin: func</code></h4>
<h5>Return values</h5>
<ul>
<li><a name="get_stdin.0"></a> own&lt;<a href="#input_stream"><a href="#input_stream"><code>input-stream</code></a></a>&gt;</li>
</ul>
<h2><a name="wasi:clocks_monotonic_clock_0.2.0"></a>Import interface wasi:clocks/monotonic-clock@0.2.0</h2>
<p>WASI Monotonic Clock is a clock API intended to let users measure elapsed
time.</p>
<p>It is intended to be portable at least between Unix-family platforms and
Windows.</p>
<p>A monotonic clock is a clock which has an unspecified initial value, and
successive reads of the clock will produce non-decreasing values.</p>
<p>It is intended for measuring elapsed time.</p>
<hr />
<h3>Types</h3>
<h4><a name="pollable"></a><code>type pollable</code></h4>
<p><a href="#pollable"><a href="#pollable"><code>pollable</code></a></a></p>
<p>
#### <a name="instant"></a>`type instant`
`u64`
<p>An instant in time, in nanoseconds. An instant is relative to an
unspecified initial value, and can only be compared to instances from
the same monotonic-clock.
<h4><a name="duration"></a><code>type duration</code></h4>
<p><code>u64</code></p>
<p>A duration of time, in nanoseconds.
<hr />
<h3>Functions</h3>
<h4><a name="now"></a><code>now: func</code></h4>
<p>Read the current value of the clock.</p>
<p>The clock is monotonic, therefore calling this function repeatedly will
produce a sequence of non-decreasing values.</p>
<h5>Return values</h5>
<ul>
<li><a name="now.0"></a> <a href="#instant"><a href="#instant"><code>instant</code></a></a></li>
</ul>
<h4><a name="resolution"></a><code>resolution: func</code></h4>
<p>Query the resolution of the clock. Returns the duration of time
corresponding to a clock tick.</p>
<h5>Return values</h5>
<ul>
<li><a name="resolution.0"></a> <a href="#duration"><a href="#duration"><code>duration</code></a></a></li>
</ul>
<h4><a name="subscribe_instant"></a><code>subscribe-instant: func</code></h4>
<p>Create a <a href="#pollable"><code>pollable</code></a> which will resolve once the specified instant
occured.</p>
<h5>Params</h5>
<ul>
<li><a name="subscribe_instant.when"></a><code>when</code>: <a href="#instant"><a href="#instant"><code>instant</code></a></a></li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="subscribe_instant.0"></a> own&lt;<a href="#pollable"><a href="#pollable"><code>pollable</code></a></a>&gt;</li>
</ul>
<h4><a name="subscribe_duration"></a><code>subscribe-duration: func</code></h4>
<p>Create a <a href="#pollable"><code>pollable</code></a> which will resolve once the given duration has
elapsed, starting at the time at which this function was called.
occured.</p>
<h5>Params</h5>
<ul>
<li><a name="subscribe_duration.when"></a><code>when</code>: <a href="#duration"><a href="#duration"><code>duration</code></a></a></li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="subscribe_duration.0"></a> own&lt;<a href="#pollable"><a href="#pollable"><code>pollable</code></a></a>&gt;</li>
</ul>
<h2><a name="wasi:http_types_0.2.0"></a>Import interface wasi:http/types@0.2.0</h2>
<p>This interface defines all of the types and methods for implementing
HTTP Requests and Responses, both incoming and outgoing, as well as
their headers, trailers, and bodies.</p>
<hr />
<h3>Types</h3>
<h4><a name="duration"></a><code>type duration</code></h4>
<p><a href="#duration"><a href="#duration"><code>duration</code></a></a></p>
<p>
#### <a name="input_stream"></a>`type input-stream`
[`input-stream`](#input_stream)
<p>
#### <a name="output_stream"></a>`type output-stream`
[`output-stream`](#output_stream)
<p>
#### <a name="io_error"></a>`type io-error`
[`error`](#error)
<p>
#### <a name="pollable"></a>`type pollable`
[`pollable`](#pollable)
<p>
#### <a name="method"></a>`variant method`
<p>This type corresponds to HTTP standard Methods.</p>
<h5>Variant Cases</h5>
<ul>
<li><a name="method.get"></a><a href="#get"><code>get</code></a></li>
<li><a name="method.head"></a><code>head</code></li>
<li><a name="method.post"></a><code>post</code></li>
<li><a name="method.put"></a><code>put</code></li>
<li><a name="method.delete"></a><a href="#delete"><code>delete</code></a></li>
<li><a name="method.connect"></a><code>connect</code></li>
<li><a name="method.options"></a><code>options</code></li>
<li><a name="method.trace"></a><code>trace</code></li>
<li><a name="method.patch"></a><code>patch</code></li>
<li><a name="method.other"></a><code>other</code>: <code>string</code></li>
</ul>
<h4><a name="scheme"></a><code>variant scheme</code></h4>
<p>This type corresponds to HTTP standard Related Schemes.</p>
<h5>Variant Cases</h5>
<ul>
<li><a name="scheme.http"></a><code>HTTP</code></li>
<li><a name="scheme.https"></a><code>HTTPS</code></li>
<li><a name="scheme.other"></a><code>other</code>: <code>string</code></li>
</ul>
<h4><a name="dns_error_payload"></a><code>record DNS-error-payload</code></h4>
<p>Defines the case payload type for <code>DNS-error</code> above:</p>
<h5>Record Fields</h5>
<ul>
<li><a name="dns_error_payload.rcode"></a><code>rcode</code>: option&lt;<code>string</code>&gt;</li>
<li><a name="dns_error_payload.info_code"></a><code>info-code</code>: option&lt;<code>u16</code>&gt;</li>
</ul>
<h4><a name="tls_alert_received_payload"></a><code>record TLS-alert-received-payload</code></h4>
<p>Defines the case payload type for <code>TLS-alert-received</code> above:</p>
<h5>Record Fields</h5>
<ul>
<li><a name="tls_alert_received_payload.alert_id"></a><code>alert-id</code>: option&lt;<code>u8</code>&gt;</li>
<li><a name="tls_alert_received_payload.alert_message"></a><code>alert-message</code>: option&lt;<code>string</code>&gt;</li>
</ul>
<h4><a name="field_size_payload"></a><code>record field-size-payload</code></h4>
<p>Defines the case payload type for <code>HTTP-response-{header,trailer}-size</code> above:</p>
<h5>Record Fields</h5>
<ul>
<li><a name="field_size_payload.field_name"></a><code>field-name</code>: option&lt;<code>string</code>&gt;</li>
<li><a name="field_size_payload.field_size"></a><code>field-size</code>: option&lt;<code>u32</code>&gt;</li>
</ul>
<h4><a name="error_code"></a><code>variant error-code</code></h4>
<p>These cases are inspired by the IANA HTTP Proxy Error Types:
https://www.iana.org/assignments/http-proxy-status/http-proxy-status.xhtml#table-http-proxy-error-types</p>
<h5>Variant Cases</h5>
<ul>
<li><a name="error_code.dns_timeout"></a><code>DNS-timeout</code></li>
<li><a name="error_code.dns_error"></a><code>DNS-error</code>: <a href="#dns_error_payload"><a href="#dns_error_payload"><code>DNS-error-payload</code></a></a></li>
<li><a name="error_code.destination_not_found"></a><code>destination-not-found</code></li>
<li><a name="error_code.destination_unavailable"></a><code>destination-unavailable</code></li>
<li><a name="error_code.destination_ip_prohibited"></a><code>destination-IP-prohibited</code></li>
<li><a name="error_code.destination_ip_unroutable"></a><code>destination-IP-unroutable</code></li>
<li><a name="error_code.connection_refused"></a><code>connection-refused</code></li>
<li><a name="error_code.connection_terminated"></a><code>connection-terminated</code></li>
<li><a name="error_code.connection_timeout"></a><code>connection-timeout</code></li>
<li><a name="error_code.connection_read_timeout"></a><code>connection-read-timeout</code></li>
<li><a name="error_code.connection_write_timeout"></a><code>connection-write-timeout</code></li>
<li><a name="error_code.connection_limit_reached"></a><code>connection-limit-reached</code></li>
<li><a name="error_code.tls_protocol_error"></a><code>TLS-protocol-error</code></li>
<li><a name="error_code.tls_certificate_error"></a><code>TLS-certificate-error</code></li>
<li><a name="error_code.tls_alert_received"></a><code>TLS-alert-received</code>: <a href="#tls_alert_received_payload"><a href="#tls_alert_received_payload"><code>TLS-alert-received-payload</code></a></a></li>
<li><a name="error_code.http_request_denied"></a><code>HTTP-request-denied</code></li>
<li><a name="error_code.http_request_length_required"></a><code>HTTP-request-length-required</code></li>
<li><a name="error_code.http_request_body_size"></a><code>HTTP-request-body-size</code>: option&lt;<code>u64</code>&gt;</li>
<li><a name="error_code.http_request_method_invalid"></a><code>HTTP-request-method-invalid</code></li>
<li><a name="error_code.http_request_uri_invalid"></a><code>HTTP-request-URI-invalid</code></li>
<li><a name="error_code.http_request_uri_too_long"></a><code>HTTP-request-URI-too-long</code></li>
<li><a name="error_code.http_request_header_section_size"></a><code>HTTP-request-header-section-size</code>: option&lt;<code>u32</code>&gt;</li>
<li><a name="error_code.http_request_header_size"></a><code>HTTP-request-header-size</code>: option&lt;<a href="#field_size_payload"><a href="#field_size_payload"><code>field-size-payload</code></a></a>&gt;</li>
<li><a name="error_code.http_request_trailer_section_size"></a><code>HTTP-request-trailer-section-size</code>: option&lt;<code>u32</code>&gt;</li>
<li><a name="error_code.http_request_trailer_size"></a><code>HTTP-request-trailer-size</code>: <a href="#field_size_payload"><a href="#field_size_payload"><code>field-size-payload</code></a></a></li>
<li><a name="error_code.http_response_incomplete"></a><code>HTTP-response-incomplete</code></li>
<li><a name="error_code.http_response_header_section_size"></a><code>HTTP-response-header-section-size</code>: option&lt;<code>u32</code>&gt;</li>
<li><a name="error_code.http_response_header_size"></a><code>HTTP-response-header-size</code>: <a href="#field_size_payload"><a href="#field_size_payload"><code>field-size-payload</code></a></a></li>
<li><a name="error_code.http_response_body_size"></a><code>HTTP-response-body-size</code>: option&lt;<code>u64</code>&gt;</li>
<li><a name="error_code.http_response_trailer_section_size"></a><code>HTTP-response-trailer-section-size</code>: option&lt;<code>u32</code>&gt;</li>
<li><a name="error_code.http_response_trailer_size"></a><code>HTTP-response-trailer-size</code>: <a href="#field_size_payload"><a href="#field_size_payload"><code>field-size-payload</code></a></a></li>
<li><a name="error_code.http_response_transfer_coding"></a><code>HTTP-response-transfer-coding</code>: option&lt;<code>string</code>&gt;</li>
<li><a name="error_code.http_response_content_coding"></a><code>HTTP-response-content-coding</code>: option&lt;<code>string</code>&gt;</li>
<li><a name="error_code.http_response_timeout"></a><code>HTTP-response-timeout</code></li>
<li><a name="error_code.http_upgrade_failed"></a><code>HTTP-upgrade-failed</code></li>
<li><a name="error_code.http_protocol_error"></a><code>HTTP-protocol-error</code></li>
<li><a name="error_code.loop_detected"></a><code>loop-detected</code></li>
<li><a name="error_code.configuration_error"></a><code>configuration-error</code></li>
<li><a name="error_code.internal_error"></a><code>internal-error</code>: option&lt;<code>string</code>&gt;<p>This is a catch-all error for anything that doesn't fit cleanly into a
more specific case. It also includes an optional string for an
unstructured description of the error. Users should not depend on the
string for diagnosing errors, as it's not required to be consistent
between implementations.
</li>
</ul>
<h4><a name="header_error"></a><code>variant header-error</code></h4>
<p>This type enumerates the different kinds of errors that may occur when
setting or appending to a <a href="#fields"><code>fields</code></a> resource.</p>
<h5>Variant Cases</h5>
<ul>
<li>
<p><a name="header_error.invalid_syntax"></a><code>invalid-syntax</code></p>
<p>This error indicates that a `field-key` or `field-value` was
syntactically invalid when used with an operation that sets headers in a
`fields`.
</li>
<li>
<p><a name="header_error.forbidden"></a><code>forbidden</code></p>
<p>This error indicates that a forbidden `field-key` was used when trying
to set a header in a `fields`.
</li>
<li>
<p><a name="header_error.immutable"></a><code>immutable</code></p>
<p>This error indicates that the operation on the `fields` was not
permitted because the fields are immutable.
</li>
</ul>
<h4><a name="field_key"></a><code>type field-key</code></h4>
<p><code>string</code></p>
<p>Field keys are always strings.
<h4><a name="field_value"></a><code>type field-value</code></h4>
<p><a href="#field_value"><a href="#field_value"><code>field-value</code></a></a></p>
<p>Field values should always be ASCII strings. However, in
reality, HTTP implementations often have to interpret malformed values,
so they are provided as a list of bytes.
<h4><a name="fields"></a><code>resource fields</code></h4>
<p>This following block defines the <a href="#fields"><code>fields</code></a> resource which corresponds to
HTTP standard Fields. Fields are a common representation used for both
Headers and Trailers.</p>
<p>A <a href="#fields"><code>fields</code></a> may be mutable or immutable. A <a href="#fields"><code>fields</code></a> created using the
constructor, <code>from-list</code>, or <code>clone</code> will be mutable, but a <a href="#fields"><code>fields</code></a>
resource given by other means (including, but not limited to,
<code>incoming-request.headers</code>, <code>outgoing-request.headers</code>) might be be
immutable. In an immutable fields, the <a href="#set"><code>set</code></a>, <code>append</code>, and <a href="#delete"><code>delete</code></a>
operations will fail with <code>header-error.immutable</code>.</p>
<h4><a name="headers"></a><code>type headers</code></h4>
<p><a href="#fields"><a href="#fields"><code>fields</code></a></a></p>
<p>Headers is an alias for Fields.
<h4><a name="trailers"></a><code>type trailers</code></h4>
<p><a href="#fields"><a href="#fields"><code>fields</code></a></a></p>
<p>Trailers is an alias for Fields.
<h4><a name="incoming_request"></a><code>resource incoming-request</code></h4>
<p>Represents an incoming HTTP Request.</p>
<h4><a name="outgoing_request"></a><code>resource outgoing-request</code></h4>
<p>Represents an outgoing HTTP Request.</p>
<h4><a name="request_options"></a><code>resource request-options</code></h4>
<p>Parameters for making an HTTP Request. Each of these parameters is
currently an optional timeout applicable to the transport layer of the
HTTP protocol.</p>
<p>These timeouts are separate from any the user may use to bound a
blocking call to <code>wasi:io/poll.poll</code>.</p>
<h4><a name="response_outparam"></a><code>resource response-outparam</code></h4>
<p>Represents the ability to send an HTTP Response.</p>
<p>This resource is used by the <code>wasi:http/incoming-handler</code> interface to
allow a Response to be sent corresponding to the Request provided as the
other argument to <code>incoming-handler.handle</code>.</p>
<h4><a name="status_code"></a><code>type status-code</code></h4>
<p><code>u16</code></p>
<p>This type corresponds to the HTTP standard Status Code.
<h4><a name="incoming_response"></a><code>resource incoming-response</code></h4>
<p>Represents an incoming HTTP Response.</p>
<h4><a name="incoming_body"></a><code>resource incoming-body</code></h4>
<p>Represents an incoming HTTP Request or Response's Body.</p>
<p>A body has both its contents - a stream of bytes - and a (possibly
empty) set of trailers, indicating that the full contents of the
body have been received. This resource represents the contents as
an <a href="#input_stream"><code>input-stream</code></a> and the delivery of trailers as a <a href="#future_trailers"><code>future-trailers</code></a>,
and ensures that the user of this interface may only be consuming either
the body contents or waiting on trailers at any given time.</p>
<h4><a name="future_trailers"></a><code>resource future-trailers</code></h4>
<p>Represents a future which may eventaully return trailers, or an error.</p>
<p>In the case that the incoming HTTP Request or Response did not have any
trailers, this future will resolve to the empty set of trailers once the
complete Request or Response body has been received.</p>
<h4><a name="outgoing_response"></a><code>resource outgoing-response</code></h4>
<p>Represents an outgoing HTTP Response.</p>
<h4><a name="outgoing_body"></a><code>resource outgoing-body</code></h4>
<p>Represents an outgoing HTTP Request or Response's Body.</p>
<p>A body has both its contents - a stream of bytes - and a (possibly
empty) set of trailers, inducating the full contents of the body
have been sent. This resource represents the contents as an
<a href="#output_stream"><code>output-stream</code></a> child resource, and the completion of the body (with
optional trailers) with a static function that consumes the
<a href="#outgoing_body"><code>outgoing-body</code></a> resource, and ensures that the user of this interface
may not write to the body contents after the body has been finished.</p>
<p>If the user code drops this resource, as opposed to calling the static
method <code>finish</code>, the implementation should treat the body as incomplete,
and that an error has occured. The implementation should propogate this
error to the HTTP protocol by whatever means it has available,
including: corrupting the body on the wire, aborting the associated
Request, or sending a late status code for the Response.</p>
<h4><a name="future_incoming_response"></a><code>resource future-incoming-response</code></h4>
<p>Represents a future which may eventaully return an incoming HTTP
Response, or an error.</p>
<h2>This resource is returned by the <code>wasi:http/outgoing-handler</code> interface to
provide the HTTP Response corresponding to the sent Request.</h2>
<h3>Functions</h3>
<h4><a name="http_error_code"></a><code>http-error-code: func</code></h4>
<p>Attempts to extract a http-related <a href="#error"><code>error</code></a> from the wasi:io <a href="#error"><code>error</code></a>
provided.</p>
<p>Stream operations which return
<code>wasi:io/stream/stream-error::last-operation-failed</code> have a payload of
type <code>wasi:io/error/error</code> with more information about the operation
that failed. This payload can be passed through to this function to see
if there's http-related information about the error to return.</p>
<p>Note that this function is fallible because not all io-errors are
http-related errors.</p>
<h5>Params</h5>
<ul>
<li><a name="http_error_code.err"></a><code>err</code>: borrow&lt;<a href="#io_error"><a href="#io_error"><code>io-error</code></a></a>&gt;</li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="http_error_code.0"></a> option&lt;<a href="#error_code"><a href="#error_code"><code>error-code</code></a></a>&gt;</li>
</ul>
<h4><a name="constructor_fields"></a><code>[constructor]fields: func</code></h4>
<p>Construct an empty HTTP Fields.</p>
<p>The resulting <a href="#fields"><code>fields</code></a> is mutable.</p>
<h5>Return values</h5>
<ul>
<li><a name="constructor_fields.0"></a> own&lt;<a href="#fields"><a href="#fields"><code>fields</code></a></a>&gt;</li>
</ul>
<h4><a name="static_fields.from_list"></a><code>[static]fields.from-list: func</code></h4>
<p>Construct an HTTP Fields.</p>
<p>The resulting <a href="#fields"><code>fields</code></a> is mutable.</p>
<p>The list represents each key-value pair in the Fields. Keys
which have multiple values are represented by multiple entries in this
list with the same key.</p>
<p>The tuple is a pair of the field key, represented as a string, and
Value, represented as a list of bytes.</p>
<p>An error result will be returned if any <a href="#field_key"><code>field-key</code></a> or <a href="#field_value"><code>field-value</code></a> is
syntactically invalid, or if a field is forbidden.</p>
<h5>Params</h5>
<ul>
<li><a name="static_fields.from_list.entries"></a><code>entries</code>: list&lt;(<a href="#field_key"><a href="#field_key"><code>field-key</code></a></a>, <a href="#field_value"><a href="#field_value"><code>field-value</code></a></a>)&gt;</li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="static_fields.from_list.0"></a> result&lt;own&lt;<a href="#fields"><a href="#fields"><code>fields</code></a></a>&gt;, <a href="#header_error"><a href="#header_error"><code>header-error</code></a></a>&gt;</li>
</ul>
<h4><a name="method_fields.get"></a><code>[method]fields.get: func</code></h4>
<p>Get all of the values corresponding to a key. If the key is not present
in this <a href="#fields"><code>fields</code></a> or is syntactically invalid, an empty list is returned.
However, if the key is present but empty, this is represented by a list
with one or more empty field-values present.</p>
<h5>Params</h5>
<ul>
<li><a name="method_fields.get.self"></a><code>self</code>: borrow&lt;<a href="#fields"><a href="#fields"><code>fields</code></a></a>&gt;</li>
<li><a name="method_fields.get.name"></a><code>name</code>: <a href="#field_key"><a href="#field_key"><code>field-key</code></a></a></li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="method_fields.get.0"></a> list&lt;<a href="#field_value"><a href="#field_value"><code>field-value</code></a></a>&gt;</li>
</ul>
<h4><a name="method_fields.has"></a><code>[method]fields.has: func</code></h4>
<p>Returns <code>true</code> when the key is present in this <a href="#fields"><code>fields</code></a>. If the key is
syntactically invalid, <code>false</code> is returned.</p>
<h5>Params</h5>
<ul>
<li><a name="method_fields.has.self"></a><code>self</code>: borrow&lt;<a href="#fields"><a href="#fields"><code>fields</code></a></a>&gt;</li>
<li><a name="method_fields.has.name"></a><code>name</code>: <a href="#field_key"><a href="#field_key"><code>field-key</code></a></a></li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="method_fields.has.0"></a> <code>bool</code></li>
</ul>
<h4><a name="method_fields.set"></a><code>[method]fields.set: func</code></h4>
<p>Set all of the values for a key. Clears any existing values for that
key, if they have been set.</p>
<p>Fails with <code>header-error.immutable</code> if the <a href="#fields"><code>fields</code></a> are immutable.</p>
<p>Fails with <code>header-error.invalid-syntax</code> if the <a href="#field_key"><code>field-key</code></a> or any of
the <a href="#field_value"><code>field-value</code></a>s are syntactically invalid.</p>
<h5>Params</h5>
<ul>
<li><a name="method_fields.set.self"></a><code>self</code>: borrow&lt;<a href="#fields"><a href="#fields"><code>fields</code></a></a>&gt;</li>
<li><a name="method_fields.set.name"></a><code>name</code>: <a href="#field_key"><a href="#field_key"><code>field-key</code></a></a></li>
<li><a name="method_fields.set.value"></a><code>value</code>: list&lt;<a href="#field_value"><a href="#field_value"><code>field-value</code></a></a>&gt;</li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="method_fields.set.0"></a> result&lt;_, <a href="#header_error"><a href="#header_error"><code>header-error</code></a></a>&gt;</li>
</ul>
<h4><a name="method_fields.delete"></a><code>[method]fields.delete: func</code></h4>
<p>Delete all values for a key. Does nothing if no values for the key
exist.</p>
<p>Fails with <code>header-error.immutable</code> if the <a href="#fields"><code>fields</code></a> are immutable.</p>
<p>Fails with <code>header-error.invalid-syntax</code> if the <a href="#field_key"><code>field-key</code></a> is
syntactically invalid.</p>
<h5>Params</h5>
<ul>
<li><a name="method_fields.delete.self"></a><code>self</code>: borrow&lt;<a href="#fields"><a href="#fields"><code>fields</code></a></a>&gt;</li>
<li><a name="method_fields.delete.name"></a><code>name</code>: <a href="#field_key"><a href="#field_key"><code>field-key</code></a></a></li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="method_fields.delete.0"></a> result&lt;_, <a href="#header_error"><a href="#header_error"><code>header-error</code></a></a>&gt;</li>
</ul>
<h4><a name="method_fields.append"></a><code>[method]fields.append: func</code></h4>
<p>Append a value for a key. Does not change or delete any existing
values for that key.</p>
<p>Fails with <code>header-error.immutable</code> if the <a href="#fields"><code>fields</code></a> are immutable.</p>
<p>Fails with <code>header-error.invalid-syntax</code> if the <a href="#field_key"><code>field-key</code></a> or
<a href="#field_value"><code>field-value</code></a> are syntactically invalid.</p>
<h5>Params</h5>
<ul>
<li><a name="method_fields.append.self"></a><code>self</code>: borrow&lt;<a href="#fields"><a href="#fields"><code>fields</code></a></a>&gt;</li>
<li><a name="method_fields.append.name"></a><code>name</code>: <a href="#field_key"><a href="#field_key"><code>field-key</code></a></a></li>
<li><a name="method_fields.append.value"></a><code>value</code>: <a href="#field_value"><a href="#field_value"><code>field-value</code></a></a></li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="method_fields.append.0"></a> result&lt;_, <a href="#header_error"><a href="#header_error"><code>header-error</code></a></a>&gt;</li>
</ul>
<h4><a name="method_fields.entries"></a><code>[method]fields.entries: func</code></h4>
<p>Retrieve the full set of keys and values in the Fields. Like the
constructor, the list represents each key-value pair.</p>
<p>The outer list represents each key-value pair in the Fields. Keys
which have multiple values are represented by multiple entries in this
list with the same key.</p>
<h5>Params</h5>
<ul>
<li><a name="method_fields.entries.self"></a><code>self</code>: borrow&lt;<a href="#fields"><a href="#fields"><code>fields</code></a></a>&gt;</li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="method_fields.entries.0"></a> list&lt;(<a href="#field_key"><a href="#field_key"><code>field-key</code></a></a>, <a href="#field_value"><a href="#field_value"><code>field-value</code></a></a>)&gt;</li>
</ul>
<h4><a name="method_fields.clone"></a><code>[method]fields.clone: func</code></h4>
<p>Make a deep copy of the Fields. Equivelant in behavior to calling the
<a href="#fields"><code>fields</code></a> constructor on the return value of <code>entries</code>. The resulting
<a href="#fields"><code>fields</code></a> is mutable.</p>
<h5>Params</h5>
<ul>
<li><a name="method_fields.clone.self"></a><code>self</code>: borrow&lt;<a href="#fields"><a href="#fields"><code>fields</code></a></a>&gt;</li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="method_fields.clone.0"></a> own&lt;<a href="#fields"><a href="#fields"><code>fields</code></a></a>&gt;</li>
</ul>
<h4><a name="method_incoming_request.method"></a><code>[method]incoming-request.method: func</code></h4>
<p>Returns the method of the incoming request.</p>
<h5>Params</h5>
<ul>
<li><a name="method_incoming_request.method.self"></a><code>self</code>: borrow&lt;<a href="#incoming_request"><a href="#incoming_request"><code>incoming-request</code></a></a>&gt;</li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="method_incoming_request.method.0"></a> <a href="#method"><a href="#method"><code>method</code></a></a></li>
</ul>
<h4><a name="method_incoming_request.path_with_query"></a><code>[method]incoming-request.path-with-query: func</code></h4>
<p>Returns the path with query parameters from the request, as a string.</p>
<h5>Params</h5>
<ul>
<li><a name="method_incoming_request.path_with_query.self"></a><code>self</code>: borrow&lt;<a href="#incoming_request"><a href="#incoming_request"><code>incoming-request</code></a></a>&gt;</li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="method_incoming_request.path_with_query.0"></a> option&lt;<code>string</code>&gt;</li>
</ul>
<h4><a name="method_incoming_request.scheme"></a><code>[method]incoming-request.scheme: func</code></h4>
<p>Returns the protocol scheme from the request.</p>
<h5>Params</h5>
<ul>
<li><a name="method_incoming_request.scheme.self"></a><code>self</code>: borrow&lt;<a href="#incoming_request"><a href="#incoming_request"><code>incoming-request</code></a></a>&gt;</li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="method_incoming_request.scheme.0"></a> option&lt;<a href="#scheme"><a href="#scheme"><code>scheme</code></a></a>&gt;</li>
</ul>
<h4><a name="method_incoming_request.authority"></a><code>[method]incoming-request.authority: func</code></h4>
<p>Returns the authority from the request, if it was present.</p>
<h5>Params</h5>
<ul>
<li><a name="method_incoming_request.authority.self"></a><code>self</code>: borrow&lt;<a href="#incoming_request"><a href="#incoming_request"><code>incoming-request</code></a></a>&gt;</li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="method_incoming_request.authority.0"></a> option&lt;<code>string</code>&gt;</li>
</ul>
<h4><a name="method_incoming_request.headers"></a><code>[method]incoming-request.headers: func</code></h4>
<p>Get the <a href="#headers"><code>headers</code></a> associated with the request.</p>
<p>The returned <a href="#headers"><code>headers</code></a> resource is immutable: <a href="#set"><code>set</code></a>, <code>append</code>, and
<a href="#delete"><code>delete</code></a> operations will fail with <code>header-error.immutable</code>.</p>
<p>The <a href="#headers"><code>headers</code></a> returned are a child resource: it must be dropped before
the parent <a href="#incoming_request"><code>incoming-request</code></a> is dropped. Dropping this
<a href="#incoming_request"><code>incoming-request</code></a> before all children are dropped will trap.</p>
<h5>Params</h5>
<ul>
<li><a name="method_incoming_request.headers.self"></a><code>self</code>: borrow&lt;<a href="#incoming_request"><a href="#incoming_request"><code>incoming-request</code></a></a>&gt;</li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="method_incoming_request.headers.0"></a> own&lt;<a href="#headers"><a href="#headers"><code>headers</code></a></a>&gt;</li>
</ul>
<h4><a name="method_incoming_request.consume"></a><code>[method]incoming-request.consume: func</code></h4>
<p>Gives the <a href="#incoming_body"><code>incoming-body</code></a> associated with this request. Will only
return success at most once, and subsequent calls will return error.</p>
<h5>Params</h5>
<ul>
<li><a name="method_incoming_request.consume.self"></a><code>self</code>: borrow&lt;<a href="#incoming_request"><a href="#incoming_request"><code>incoming-request</code></a></a>&gt;</li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="method_incoming_request.consume.0"></a> result&lt;own&lt;<a href="#incoming_body"><a href="#incoming_body"><code>incoming-body</code></a></a>&gt;&gt;</li>
</ul>
<h4><a name="constructor_outgoing_request"></a><code>[constructor]outgoing-request: func</code></h4>
<p>Construct a new <a href="#outgoing_request"><code>outgoing-request</code></a> with a default <a href="#method"><code>method</code></a> of <code>GET</code>, and
<code>none</code> values for <code>path-with-query</code>, <a href="#scheme"><code>scheme</code></a>, and <code>authority</code>.</p>
<ul>
<li><a href="#headers"><code>headers</code></a> is the HTTP Headers for the Request.</li>
</ul>
<p>It is possible to construct, or manipulate with the accessor functions
below, an <a href="#outgoing_request"><code>outgoing-request</code></a> with an invalid combination of <a href="#scheme"><code>scheme</code></a>
and <code>authority</code>, or <a href="#headers"><code>headers</code></a> which are not permitted to be sent.
It is the obligation of the <code>outgoing-handler.handle</code> implementation
to reject invalid constructions of <a href="#outgoing_request"><code>outgoing-request</code></a>.</p>
<h5>Params</h5>
<ul>
<li><a name="constructor_outgoing_request.headers"></a><a href="#headers"><code>headers</code></a>: own&lt;<a href="#headers"><a href="#headers"><code>headers</code></a></a>&gt;</li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="constructor_outgoing_request.0"></a> own&lt;<a href="#outgoing_request"><a href="#outgoing_request"><code>outgoing-request</code></a></a>&gt;</li>
</ul>
<h4><a name="method_outgoing_request.body"></a><code>[method]outgoing-request.body: func</code></h4>
<p>Returns the resource corresponding to the outgoing Body for this
Request.</p>
<p>Returns success on the first call: the <a href="#outgoing_body"><code>outgoing-body</code></a> resource for
this <a href="#outgoing_request"><code>outgoing-request</code></a> can be retrieved at most once. Subsequent
calls will return error.</p>
<h5>Params</h5>
<ul>
<li><a name="method_outgoing_request.body.self"></a><code>self</code>: borrow&lt;<a href="#outgoing_request"><a href="#outgoing_request"><code>outgoing-request</code></a></a>&gt;</li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="method_outgoing_request.body.0"></a> result&lt;own&lt;<a href="#outgoing_body"><a href="#outgoing_body"><code>outgoing-body</code></a></a>&gt;&gt;</li>
</ul>
<h4><a name="method_outgoing_request.method"></a><code>[method]outgoing-request.method: func</code></h4>
<p>Get the Method for the Request.</p>
<h5>Params</h5>
<ul>
<li><a name="method_outgoing_request.method.self"></a><code>self</code>: borrow&lt;<a href="#outgoing_request"><a href="#outgoing_request"><code>outgoing-request</code></a></a>&gt;</li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="method_outgoing_request.method.0"></a> <a href="#method"><a href="#method"><code>method</code></a></a></li>
</ul>
<h4><a name="method_outgoing_request.set_method"></a><code>[method]outgoing-request.set-method: func</code></h4>
<p>Set the Method for the Request. Fails if the string present in a
<code>method.other</code> argument is not a syntactically valid method.</p>
<h5>Params</h5>
<ul>
<li><a name="method_outgoing_request.set_method.self"></a><code>self</code>: borrow&lt;<a href="#outgoing_request"><a href="#outgoing_request"><code>outgoing-request</code></a></a>&gt;</li>
<li><a name="method_outgoing_request.set_method.method"></a><a href="#method"><code>method</code></a>: <a href="#method"><a href="#method"><code>method</code></a></a></li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="method_outgoing_request.set_method.0"></a> result</li>
</ul>
<h4><a name="method_outgoing_request.path_with_query"></a><code>[method]outgoing-request.path-with-query: func</code></h4>
<p>Get the combination of the HTTP Path and Query for the Request.
When <code>none</code>, this represents an empty Path and empty Query.</p>
<h5>Params</h5>
<ul>
<li><a name="method_outgoing_request.path_with_query.self"></a><code>self</code>: borrow&lt;<a href="#outgoing_request"><a href="#outgoing_request"><code>outgoing-request</code></a></a>&gt;</li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="method_outgoing_request.path_with_query.0"></a> option&lt;<code>string</code>&gt;</li>
</ul>
<h4><a name="method_outgoing_request.set_path_with_query"></a><code>[method]outgoing-request.set-path-with-query: func</code></h4>
<p>Set the combination of the HTTP Path and Query for the Request.
When <code>none</code>, this represents an empty Path and empty Query. Fails is the
string given is not a syntactically valid path and query uri component.</p>
<h5>Params</h5>
<ul>
<li><a name="method_outgoing_request.set_path_with_query.self"></a><code>self</code>: borrow&lt;<a href="#outgoing_request"><a href="#outgoing_request"><code>outgoing-request</code></a></a>&gt;</li>
<li><a name="method_outgoing_request.set_path_with_query.path_with_query"></a><code>path-with-query</code>: option&lt;<code>string</code>&gt;</li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="method_outgoing_request.set_path_with_query.0"></a> result</li>
</ul>
<h4><a name="method_outgoing_request.scheme"></a><code>[method]outgoing-request.scheme: func</code></h4>
<p>Get the HTTP Related Scheme for the Request. When <code>none</code>, the
implementation may choose an appropriate default scheme.</p>
<h5>Params</h5>
<ul>
<li><a name="method_outgoing_request.scheme.self"></a><code>self</code>: borrow&lt;<a href="#outgoing_request"><a href="#outgoing_request"><code>outgoing-request</code></a></a>&gt;</li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="method_outgoing_request.scheme.0"></a> option&lt;<a href="#scheme"><a href="#scheme"><code>scheme</code></a></a>&gt;</li>
</ul>
<h4><a name="method_outgoing_request.set_scheme"></a><code>[method]outgoing-request.set-scheme: func</code></h4>
<p>Set the HTTP Related Scheme for the Request. When <code>none</code>, the
implementation may choose an appropriate default scheme. Fails if the
string given is not a syntactically valid uri scheme.</p>
<h5>Params</h5>
<ul>
<li><a name="method_outgoing_request.set_scheme.self"></a><code>self</code>: borrow&lt;<a href="#outgoing_request"><a href="#outgoing_request"><code>outgoing-request</code></a></a>&gt;</li>
<li><a name="method_outgoing_request.set_scheme.scheme"></a><a href="#scheme"><code>scheme</code></a>: option&lt;<a href="#scheme"><a href="#scheme"><code>scheme</code></a></a>&gt;</li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="method_outgoing_request.set_scheme.0"></a> result</li>
</ul>
<h4><a name="method_outgoing_request.authority"></a><code>[method]outgoing-request.authority: func</code></h4>
<p>Get the HTTP Authority for the Request. A value of <code>none</code> may be used
with Related Schemes which do not require an Authority. The HTTP and
HTTPS schemes always require an authority.</p>
<h5>Params</h5>
<ul>
<li><a name="method_outgoing_request.authority.self"></a><code>self</code>: borrow&lt;<a href="#outgoing_request"><a href="#outgoing_request"><code>outgoing-request</code></a></a>&gt;</li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="method_outgoing_request.authority.0"></a> option&lt;<code>string</code>&gt;</li>
</ul>
<h4><a name="method_outgoing_request.set_authority"></a><code>[method]outgoing-request.set-authority: func</code></h4>
<p>Set the HTTP Authority for the Request. A value of <code>none</code> may be used
with Related Schemes which do not require an Authority. The HTTP and
HTTPS schemes always require an authority. Fails if the string given is
not a syntactically valid uri authority.</p>
<h5>Params</h5>
<ul>
<li><a name="method_outgoing_request.set_authority.self"></a><code>self</code>: borrow&lt;<a href="#outgoing_request"><a href="#outgoing_request"><code>outgoing-request</code></a></a>&gt;</li>
<li><a name="method_outgoing_request.set_authority.authority"></a><code>authority</code>: option&lt;<code>string</code>&gt;</li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="method_outgoing_request.set_authority.0"></a> result</li>
</ul>
<h4><a name="method_outgoing_request.headers"></a><code>[method]outgoing-request.headers: func</code></h4>
<p>Get the headers associated with the Request.</p>
<p>The returned <a href="#headers"><code>headers</code></a> resource is immutable: <a href="#set"><code>set</code></a>, <code>append</code>, and
<a href="#delete"><code>delete</code></a> operations will fail with <code>header-error.immutable</code>.</p>
<p>This headers resource is a child: it must be dropped before the parent
<a href="#outgoing_request"><code>outgoing-request</code></a> is dropped, or its ownership is transfered to
another component by e.g. <code>outgoing-handler.handle</code>.</p>
<h5>Params</h5>
<ul>
<li><a name="method_outgoing_request.headers.self"></a><code>self</code>: borrow&lt;<a href="#outgoing_request"><a href="#outgoing_request"><code>outgoing-request</code></a></a>&gt;</li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="method_outgoing_request.headers.0"></a> own&lt;<a href="#headers"><a href="#headers"><code>headers</code></a></a>&gt;</li>
</ul>
<h4><a name="constructor_request_options"></a><code>[constructor]request-options: func</code></h4>
<p>Construct a default <a href="#request_options"><code>request-options</code></a> value.</p>
<h5>Return values</h5>
<ul>
<li><a name="constructor_request_options.0"></a> own&lt;<a href="#request_options"><a href="#request_options"><code>request-options</code></a></a>&gt;</li>
</ul>
<h4><a name="method_request_options.connect_timeout"></a><code>[method]request-options.connect-timeout: func</code></h4>
<p>The timeout for the initial connect to the HTTP Server.</p>
<h5>Params</h5>
<ul>
<li><a name="method_request_options.connect_timeout.self"></a><code>self</code>: borrow&lt;<a href="#request_options"><a href="#request_options"><code>request-options</code></a></a>&gt;</li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="method_request_options.connect_timeout.0"></a> option&lt;<a href="#duration"><a href="#duration"><code>duration</code></a></a>&gt;</li>
</ul>
<h4><a name="method_request_options.set_connect_timeout"></a><code>[method]request-options.set-connect-timeout: func</code></h4>
<p>Set the timeout for the initial connect to the HTTP Server. An error
return value indicates that this timeout is not supported.</p>
<h5>Params</h5>
<ul>
<li><a name="method_request_options.set_connect_timeout.self"></a><code>self</code>: borrow&lt;<a href="#request_options"><a href="#request_options"><code>request-options</code></a></a>&gt;</li>
<li><a name="method_request_options.set_connect_timeout.duration"></a><a href="#duration"><code>duration</code></a>: option&lt;<a href="#duration"><a href="#duration"><code>duration</code></a></a>&gt;</li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="method_request_options.set_connect_timeout.0"></a> result</li>
</ul>
<h4><a name="method_request_options.first_byte_timeout"></a><code>[method]request-options.first-byte-timeout: func</code></h4>
<p>The timeout for receiving the first byte of the Response body.</p>
<h5>Params</h5>
<ul>
<li><a name="method_request_options.first_byte_timeout.self"></a><code>self</code>: borrow&lt;<a href="#request_options"><a href="#request_options"><code>request-options</code></a></a>&gt;</li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="method_request_options.first_byte_timeout.0"></a> option&lt;<a href="#duration"><a href="#duration"><code>duration</code></a></a>&gt;</li>
</ul>
<h4><a name="method_request_options.set_first_byte_timeout"></a><code>[method]request-options.set-first-byte-timeout: func</code></h4>
<p>Set the timeout for receiving the first byte of the Response body. An
error return value indicates that this timeout is not supported.</p>
<h5>Params</h5>
<ul>
<li><a name="method_request_options.set_first_byte_timeout.self"></a><code>self</code>: borrow&lt;<a href="#request_options"><a href="#request_options"><code>request-options</code></a></a>&gt;</li>
<li><a name="method_request_options.set_first_byte_timeout.duration"></a><a href="#duration"><code>duration</code></a>: option&lt;<a href="#duration"><a href="#duration"><code>duration</code></a></a>&gt;</li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="method_request_options.set_first_byte_timeout.0"></a> result</li>
</ul>
<h4><a name="method_request_options.between_bytes_timeout"></a><code>[method]request-options.between-bytes-timeout: func</code></h4>
<p>The timeout for receiving subsequent chunks of bytes in the Response
body stream.</p>
<h5>Params</h5>
<ul>
<li><a name="method_request_options.between_bytes_timeout.self"></a><code>self</code>: borrow&lt;<a href="#request_options"><a href="#request_options"><code>request-options</code></a></a>&gt;</li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="method_request_options.between_bytes_timeout.0"></a> option&lt;<a href="#duration"><a href="#duration"><code>duration</code></a></a>&gt;</li>
</ul>
<h4><a name="method_request_options.set_between_bytes_timeout"></a><code>[method]request-options.set-between-bytes-timeout: func</code></h4>
<p>Set the timeout for receiving subsequent chunks of bytes in the Response
body stream. An error return value indicates that this timeout is not
supported.</p>
<h5>Params</h5>
<ul>
<li><a name="method_request_options.set_between_bytes_timeout.self"></a><code>self</code>: borrow&lt;<a href="#request_options"><a href="#request_options"><code>request-options</code></a></a>&gt;</li>
<li><a name="method_request_options.set_between_bytes_timeout.duration"></a><a href="#duration"><code>duration</code></a>: option&lt;<a href="#duration"><a href="#duration"><code>duration</code></a></a>&gt;</li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="method_request_options.set_between_bytes_timeout.0"></a> result</li>
</ul>
<h4><a name="static_response_outparam.set"></a><code>[static]response-outparam.set: func</code></h4>
<p>Set the value of the <a href="#response_outparam"><code>response-outparam</code></a> to either send a response,
or indicate an error.</p>
<p>This method consumes the <a href="#response_outparam"><code>response-outparam</code></a> to ensure that it is
called at most once. If it is never called, the implementation
will respond with an error.</p>
<p>The user may provide an <a href="#error"><code>error</code></a> to <code>response</code> to allow the
implementation determine how to respond with an HTTP error response.</p>
<h5>Params</h5>
<ul>
<li><a name="static_response_outparam.set.param"></a><code>param</code>: own&lt;<a href="#response_outparam"><a href="#response_outparam"><code>response-outparam</code></a></a>&gt;</li>
<li><a name="static_response_outparam.set.response"></a><code>response</code>: result&lt;own&lt;<a href="#outgoing_response"><a href="#outgoing_response"><code>outgoing-response</code></a></a>&gt;, <a href="#error_code"><a href="#error_code"><code>error-code</code></a></a>&gt;</li>
</ul>
<h4><a name="method_incoming_response.status"></a><code>[method]incoming-response.status: func</code></h4>
<p>Returns the status code from the incoming response.</p>
<h5>Params</h5>
<ul>
<li><a name="method_incoming_response.status.self"></a><code>self</code>: borrow&lt;<a href="#incoming_response"><a href="#incoming_response"><code>incoming-response</code></a></a>&gt;</li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="method_incoming_response.status.0"></a> <a href="#status_code"><a href="#status_code"><code>status-code</code></a></a></li>
</ul>
<h4><a name="method_incoming_response.headers"></a><code>[method]incoming-response.headers: func</code></h4>
<p>Returns the headers from the incoming response.</p>
<p>The returned <a href="#headers"><code>headers</code></a> resource is immutable: <a href="#set"><code>set</code></a>, <code>append</code>, and
<a href="#delete"><code>delete</code></a> operations will fail with <code>header-error.immutable</code>.</p>
<p>This headers resource is a child: it must be dropped before the parent
<a href="#incoming_response"><code>incoming-response</code></a> is dropped.</p>
<h5>Params</h5>
<ul>
<li><a name="method_incoming_response.headers.self"></a><code>self</code>: borrow&lt;<a href="#incoming_response"><a href="#incoming_response"><code>incoming-response</code></a></a>&gt;</li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="method_incoming_response.headers.0"></a> own&lt;<a href="#headers"><a href="#headers"><code>headers</code></a></a>&gt;</li>
</ul>
<h4><a name="method_incoming_response.consume"></a><code>[method]incoming-response.consume: func</code></h4>
<p>Returns the incoming body. May be called at most once. Returns error
if called additional times.</p>
<h5>Params</h5>
<ul>
<li><a name="method_incoming_response.consume.self"></a><code>self</code>: borrow&lt;<a href="#incoming_response"><a href="#incoming_response"><code>incoming-response</code></a></a>&gt;</li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="method_incoming_response.consume.0"></a> result&lt;own&lt;<a href="#incoming_body"><a href="#incoming_body"><code>incoming-body</code></a></a>&gt;&gt;</li>
</ul>
<h4><a name="method_incoming_body.stream"></a><code>[method]incoming-body.stream: func</code></h4>
<p>Returns the contents of the body, as a stream of bytes.</p>
<p>Returns success on first call: the stream representing the contents
can be retrieved at most once. Subsequent calls will return error.</p>
<p>The returned <a href="#input_stream"><code>input-stream</code></a> resource is a child: it must be dropped
before the parent <a href="#incoming_body"><code>incoming-body</code></a> is dropped, or consumed by
<code>incoming-body.finish</code>.</p>
<p>This invariant ensures that the implementation can determine whether
the user is consuming the contents of the body, waiting on the
<a href="#future_trailers"><code>future-trailers</code></a> to be ready, or neither. This allows for network
backpressure is to be applied when the user is consuming the body,
and for that backpressure to not inhibit delivery of the trailers if
the user does not read the entire body.</p>
<h5>Params</h5>
<ul>
<li><a name="method_incoming_body.stream.self"></a><code>self</code>: borrow&lt;<a href="#incoming_body"><a href="#incoming_body"><code>incoming-body</code></a></a>&gt;</li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="method_incoming_body.stream.0"></a> result&lt;own&lt;<a href="#input_stream"><a href="#input_stream"><code>input-stream</code></a></a>&gt;&gt;</li>
</ul>
<h4><a name="static_incoming_body.finish"></a><code>[static]incoming-body.finish: func</code></h4>
<p>Takes ownership of <a href="#incoming_body"><code>incoming-body</code></a>, and returns a <a href="#future_trailers"><code>future-trailers</code></a>.
This function will trap if the <a href="#input_stream"><code>input-stream</code></a> child is still alive.</p>
<h5>Params</h5>
<ul>
<li><a name="static_incoming_body.finish.this"></a><code>this</code>: own&lt;<a href="#incoming_body"><a href="#incoming_body"><code>incoming-body</code></a></a>&gt;</li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="static_incoming_body.finish.0"></a> own&lt;<a href="#future_trailers"><a href="#future_trailers"><code>future-trailers</code></a></a>&gt;</li>
</ul>
<h4><a name="method_future_trailers.subscribe"></a><code>[method]future-trailers.subscribe: func</code></h4>
<p>Returns a pollable which becomes ready when either the trailers have
been received, or an error has occured. When this pollable is ready,
the <a href="#get"><code>get</code></a> method will return <code>some</code>.</p>
<h5>Params</h5>
<ul>
<li><a name="method_future_trailers.subscribe.self"></a><code>self</code>: borrow&lt;<a href="#future_trailers"><a href="#future_trailers"><code>future-trailers</code></a></a>&gt;</li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="method_future_trailers.subscribe.0"></a> own&lt;<a href="#pollable"><a href="#pollable"><code>pollable</code></a></a>&gt;</li>
</ul>
<h4><a name="method_future_trailers.get"></a><code>[method]future-trailers.get: func</code></h4>
<p>Returns the contents of the trailers, or an error which occured,
once the future is ready.</p>
<p>The outer <code>option</code> represents future readiness. Users can wait on this
<code>option</code> to become <code>some</code> using the <code>subscribe</code> method.</p>
<p>The outer <code>result</code> is used to retrieve the trailers or error at most
once. It will be success on the first call in which the outer option
is <code>some</code>, and error on subsequent calls.</p>
<p>The inner <code>result</code> represents that either the HTTP Request or Response
body, as well as any trailers, were received successfully, or that an
error occured receiving them. The optional <a href="#trailers"><code>trailers</code></a> indicates whether
or not trailers were present in the body.</p>
<p>When some <a href="#trailers"><code>trailers</code></a> are returned by this method, the <a href="#trailers"><code>trailers</code></a>
resource is immutable, and a child. Use of the <a href="#set"><code>set</code></a>, <code>append</code>, or
<a href="#delete"><code>delete</code></a> methods will return an error, and the resource must be
dropped before the parent <a href="#future_trailers"><code>future-trailers</code></a> is dropped.</p>
<h5>Params</h5>
<ul>
<li><a name="method_future_trailers.get.self"></a><code>self</code>: borrow&lt;<a href="#future_trailers"><a href="#future_trailers"><code>future-trailers</code></a></a>&gt;</li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="method_future_trailers.get.0"></a> option&lt;result&lt;result&lt;option&lt;own&lt;<a href="#trailers"><a href="#trailers"><code>trailers</code></a></a>&gt;&gt;, <a href="#error_code"><a href="#error_code"><code>error-code</code></a></a>&gt;&gt;&gt;</li>
</ul>
<h4><a name="constructor_outgoing_response"></a><code>[constructor]outgoing-response: func</code></h4>
<p>Construct an <a href="#outgoing_response"><code>outgoing-response</code></a>, with a default <a href="#status_code"><code>status-code</code></a> of <code>200</code>.
If a different <a href="#status_code"><code>status-code</code></a> is needed, it must be set via the
<code>set-status-code</code> method.</p>
<ul>
<li><a href="#headers"><code>headers</code></a> is the HTTP Headers for the Response.</li>
</ul>
<h5>Params</h5>
<ul>
<li><a name="constructor_outgoing_response.headers"></a><a href="#headers"><code>headers</code></a>: own&lt;<a href="#headers"><a href="#headers"><code>headers</code></a></a>&gt;</li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="constructor_outgoing_response.0"></a> own&lt;<a href="#outgoing_response"><a href="#outgoing_response"><code>outgoing-response</code></a></a>&gt;</li>
</ul>
<h4><a name="method_outgoing_response.status_code"></a><code>[method]outgoing-response.status-code: func</code></h4>
<p>Get the HTTP Status Code for the Response.</p>
<h5>Params</h5>
<ul>
<li><a name="method_outgoing_response.status_code.self"></a><code>self</code>: borrow&lt;<a href="#outgoing_response"><a href="#outgoing_response"><code>outgoing-response</code></a></a>&gt;</li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="method_outgoing_response.status_code.0"></a> <a href="#status_code"><a href="#status_code"><code>status-code</code></a></a></li>
</ul>
<h4><a name="method_outgoing_response.set_status_code"></a><code>[method]outgoing-response.set-status-code: func</code></h4>
<p>Set the HTTP Status Code for the Response. Fails if the status-code
given is not a valid http status code.</p>
<h5>Params</h5>
<ul>
<li><a name="method_outgoing_response.set_status_code.self"></a><code>self</code>: borrow&lt;<a href="#outgoing_response"><a href="#outgoing_response"><code>outgoing-response</code></a></a>&gt;</li>
<li><a name="method_outgoing_response.set_status_code.status_code"></a><a href="#status_code"><code>status-code</code></a>: <a href="#status_code"><a href="#status_code"><code>status-code</code></a></a></li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="method_outgoing_response.set_status_code.0"></a> result</li>
</ul>
<h4><a name="method_outgoing_response.headers"></a><code>[method]outgoing-response.headers: func</code></h4>
<p>Get the headers associated with the Request.</p>
<p>The returned <a href="#headers"><code>headers</code></a> resource is immutable: <a href="#set"><code>set</code></a>, <code>append</code>, and
<a href="#delete"><code>delete</code></a> operations will fail with <code>header-error.immutable</code>.</p>
<p>This headers resource is a child: it must be dropped before the parent
<a href="#outgoing_request"><code>outgoing-request</code></a> is dropped, or its ownership is transfered to
another component by e.g. <code>outgoing-handler.handle</code>.</p>
<h5>Params</h5>
<ul>
<li><a name="method_outgoing_response.headers.self"></a><code>self</code>: borrow&lt;<a href="#outgoing_response"><a href="#outgoing_response"><code>outgoing-response</code></a></a>&gt;</li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="method_outgoing_response.headers.0"></a> own&lt;<a href="#headers"><a href="#headers"><code>headers</code></a></a>&gt;</li>
</ul>
<h4><a name="method_outgoing_response.body"></a><code>[method]outgoing-response.body: func</code></h4>
<p>Returns the resource corresponding to the outgoing Body for this Response.</p>
<p>Returns success on the first call: the <a href="#outgoing_body"><code>outgoing-body</code></a> resource for
this <a href="#outgoing_response"><code>outgoing-response</code></a> can be retrieved at most once. Subsequent
calls will return error.</p>
<h5>Params</h5>
<ul>
<li><a name="method_outgoing_response.body.self"></a><code>self</code>: borrow&lt;<a href="#outgoing_response"><a href="#outgoing_response"><code>outgoing-response</code></a></a>&gt;</li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="method_outgoing_response.body.0"></a> result&lt;own&lt;<a href="#outgoing_body"><a href="#outgoing_body"><code>outgoing-body</code></a></a>&gt;&gt;</li>
</ul>
<h4><a name="method_outgoing_body.write"></a><code>[method]outgoing-body.write: func</code></h4>
<p>Returns a stream for writing the body contents.</p>
<p>The returned <a href="#output_stream"><code>output-stream</code></a> is a child resource: it must be dropped
before the parent <a href="#outgoing_body"><code>outgoing-body</code></a> resource is dropped (or finished),
otherwise the <a href="#outgoing_body"><code>outgoing-body</code></a> drop or <code>finish</code> will trap.</p>
<p>Returns success on the first call: the <a href="#output_stream"><code>output-stream</code></a> resource for
this <a href="#outgoing_body"><code>outgoing-body</code></a> may be retrieved at most once. Subsequent calls
will return error.</p>
<h5>Params</h5>
<ul>
<li><a name="method_outgoing_body.write.self"></a><code>self</code>: borrow&lt;<a href="#outgoing_body"><a href="#outgoing_body"><code>outgoing-body</code></a></a>&gt;</li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="method_outgoing_body.write.0"></a> result&lt;own&lt;<a href="#output_stream"><a href="#output_stream"><code>output-stream</code></a></a>&gt;&gt;</li>
</ul>
<h4><a name="static_outgoing_body.finish"></a><code>[static]outgoing-body.finish: func</code></h4>
<p>Finalize an outgoing body, optionally providing trailers. This must be
called to signal that the response is complete. If the <a href="#outgoing_body"><code>outgoing-body</code></a>
is dropped without calling <code>outgoing-body.finalize</code>, the implementation
should treat the body as corrupted.</p>
<p>Fails if the body's <a href="#outgoing_request"><code>outgoing-request</code></a> or <a href="#outgoing_response"><code>outgoing-response</code></a> was
constructed with a Content-Length header, and the contents written
to the body (via <code>write</code>) does not match the value given in the
Content-Length.</p>
<h5>Params</h5>
<ul>
<li><a name="static_outgoing_body.finish.this"></a><code>this</code>: own&lt;<a href="#outgoing_body"><a href="#outgoing_body"><code>outgoing-body</code></a></a>&gt;</li>
<li><a name="static_outgoing_body.finish.trailers"></a><a href="#trailers"><code>trailers</code></a>: option&lt;own&lt;<a href="#trailers"><a href="#trailers"><code>trailers</code></a></a>&gt;&gt;</li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="static_outgoing_body.finish.0"></a> result&lt;_, <a href="#error_code"><a href="#error_code"><code>error-code</code></a></a>&gt;</li>
</ul>
<h4><a name="method_future_incoming_response.subscribe"></a><code>[method]future-incoming-response.subscribe: func</code></h4>
<p>Returns a pollable which becomes ready when either the Response has
been received, or an error has occured. When this pollable is ready,
the <a href="#get"><code>get</code></a> method will return <code>some</code>.</p>
<h5>Params</h5>
<ul>
<li><a name="method_future_incoming_response.subscribe.self"></a><code>self</code>: borrow&lt;<a href="#future_incoming_response"><a href="#future_incoming_response"><code>future-incoming-response</code></a></a>&gt;</li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="method_future_incoming_response.subscribe.0"></a> own&lt;<a href="#pollable"><a href="#pollable"><code>pollable</code></a></a>&gt;</li>
</ul>
<h4><a name="method_future_incoming_response.get"></a><code>[method]future-incoming-response.get: func</code></h4>
<p>Returns the incoming HTTP Response, or an error, once one is ready.</p>
<p>The outer <code>option</code> represents future readiness. Users can wait on this
<code>option</code> to become <code>some</code> using the <code>subscribe</code> method.</p>
<p>The outer <code>result</code> is used to retrieve the response or error at most
once. It will be success on the first call in which the outer option
is <code>some</code>, and error on subsequent calls.</p>
<p>The inner <code>result</code> represents that either the incoming HTTP Response
status and headers have recieved successfully, or that an error
occured. Errors may also occur while consuming the response body,
but those will be reported by the <a href="#incoming_body"><code>incoming-body</code></a> and its
<a href="#output_stream"><code>output-stream</code></a> child.</p>
<h5>Params</h5>
<ul>
<li><a name="method_future_incoming_response.get.self"></a><code>self</code>: borrow&lt;<a href="#future_incoming_response"><a href="#future_incoming_response"><code>future-incoming-response</code></a></a>&gt;</li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="method_future_incoming_response.get.0"></a> option&lt;result&lt;result&lt;own&lt;<a href="#incoming_response"><a href="#incoming_response"><code>incoming-response</code></a></a>&gt;, <a href="#error_code"><a href="#error_code"><code>error-code</code></a></a>&gt;&gt;&gt;</li>
</ul>
<h2><a name="wasi:http_outgoing_handler_0.2.0"></a>Import interface wasi:http/outgoing-handler@0.2.0</h2>
<p>This interface defines a handler of outgoing HTTP Requests. It should be
imported by components which wish to make HTTP Requests.</p>
<hr />
<h3>Types</h3>
<h4><a name="outgoing_request"></a><code>type outgoing-request</code></h4>
<p><a href="#outgoing_request"><a href="#outgoing_request"><code>outgoing-request</code></a></a></p>
<p>
#### <a name="request_options"></a>`type request-options`
[`request-options`](#request_options)
<p>
#### <a name="future_incoming_response"></a>`type future-incoming-response`
[`future-incoming-response`](#future_incoming_response)
<p>
#### <a name="error_code"></a>`type error-code`
[`error-code`](#error_code)
<p>
----
<h3>Functions</h3>
<h4><a name="handle"></a><code>handle: func</code></h4>
<p>This function is invoked with an outgoing HTTP Request, and it returns
a resource <a href="#future_incoming_response"><code>future-incoming-response</code></a> which represents an HTTP Response
which may arrive in the future.</p>
<p>The <code>options</code> argument accepts optional parameters for the HTTP
protocol's transport layer.</p>
<p>This function may return an error if the <a href="#outgoing_request"><code>outgoing-request</code></a> is invalid
or not allowed to be made. Otherwise, protocol errors are reported
through the <a href="#future_incoming_response"><code>future-incoming-response</code></a>.</p>
<h5>Params</h5>
<ul>
<li><a name="handle.request"></a><code>request</code>: own&lt;<a href="#outgoing_request"><a href="#outgoing_request"><code>outgoing-request</code></a></a>&gt;</li>
<li><a name="handle.options"></a><code>options</code>: option&lt;own&lt;<a href="#request_options"><a href="#request_options"><code>request-options</code></a></a>&gt;&gt;</li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="handle.0"></a> result&lt;own&lt;<a href="#future_incoming_response"><a href="#future_incoming_response"><code>future-incoming-response</code></a></a>&gt;, <a href="#error_code"><a href="#error_code"><code>error-code</code></a></a>&gt;</li>
</ul>
<h2><a name="wasi:clocks_wall_clock_0.2.0"></a>Import interface wasi:clocks/wall-clock@0.2.0</h2>
<p>WASI Wall Clock is a clock API intended to let users query the current
time. The name &quot;wall&quot; makes an analogy to a &quot;clock on the wall&quot;, which
is not necessarily monotonic as it may be reset.</p>
<p>It is intended to be portable at least between Unix-family platforms and
Windows.</p>
<p>A wall clock is a clock which measures the date and time according to
some external reference.</p>
<p>External references may be reset, so this clock is not necessarily
monotonic, making it unsuitable for measuring elapsed time.</p>
<p>It is intended for reporting the current date and time for humans.</p>
<hr />
<h3>Types</h3>
<h4><a name="datetime"></a><code>record datetime</code></h4>
<p>A time and date in seconds plus nanoseconds.</p>
<h5>Record Fields</h5>
<ul>
<li><a name="datetime.seconds"></a><code>seconds</code>: <code>u64</code></li>
<li><a name="datetime.nanoseconds"></a><code>nanoseconds</code>: <code>u32</code></li>
</ul>
<hr />
<h3>Functions</h3>
<h4><a name="now"></a><code>now: func</code></h4>
<p>Read the current value of the clock.</p>
<p>This clock is not monotonic, therefore calling this function repeatedly
will not necessarily produce a sequence of non-decreasing values.</p>
<p>The returned timestamps represent the number of seconds since
1970-01-01T00:00:00Z, also known as <a href="https://pubs.opengroup.org/onlinepubs/9699919799/xrat/V4_xbd_chap04.html#tag_21_04_16">POSIX's Seconds Since the Epoch</a>,
also known as <a href="https://en.wikipedia.org/wiki/Unix_time">Unix Time</a>.</p>
<p>The nanoseconds field of the output is always less than 1000000000.</p>
<h5>Return values</h5>
<ul>
<li><a name="now.0"></a> <a href="#datetime"><a href="#datetime"><code>datetime</code></a></a></li>
</ul>
<h4><a name="resolution"></a><code>resolution: func</code></h4>
<p>Query the resolution of the clock.</p>
<p>The nanoseconds field of the output is always less than 1000000000.</p>
<h5>Return values</h5>
<ul>
<li><a name="resolution.0"></a> <a href="#datetime"><a href="#datetime"><code>datetime</code></a></a></li>
</ul>
<h2><a name="wasi:http_incoming_handler_0.2.0"></a>Export interface wasi:http/incoming-handler@0.2.0</h2>
<hr />
<h3>Types</h3>
<h4><a name="incoming_request"></a><code>type incoming-request</code></h4>
<p><a href="#incoming_request"><a href="#incoming_request"><code>incoming-request</code></a></a></p>
<p>
#### <a name="response_outparam"></a>`type response-outparam`
[`response-outparam`](#response_outparam)
<p>
----
<h3>Functions</h3>
<h4><a name="handle"></a><code>handle: func</code></h4>
<p>This function is invoked with an incoming HTTP Request, and a resource
<a href="#response_outparam"><code>response-outparam</code></a> which provides the capability to reply with an HTTP
Response. The response is sent by calling the <code>response-outparam.set</code>
method, which allows execution to continue after the response has been
sent. This enables both streaming to the response body, and performing other
work.</p>
<p>The implementor of this function must write a response to the
<a href="#response_outparam"><code>response-outparam</code></a> before returning, or else the caller will respond
with an error on its behalf.</p>
<h5>Params</h5>
<ul>
<li><a name="handle.request"></a><code>request</code>: own&lt;<a href="#incoming_request"><a href="#incoming_request"><code>incoming-request</code></a></a>&gt;</li>
<li><a name="handle.response_out"></a><code>response-out</code>: own&lt;<a href="#response_outparam"><a href="#response_outparam"><code>response-outparam</code></a></a>&gt;</li>
</ul>
