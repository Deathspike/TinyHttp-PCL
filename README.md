# TinyHttp-PCL

A tiny HTTP abstraction layer for PCL. 

## Reason 

HTTP in PCL is not standard yet. This abstraction uses a WebRequest and will set headers through reflection, whie using SharpZLib for decompression of gzip and deflate streams. The result is a 100% managed tiny abstraction that will work across platforms (SL 4.0+, WP 7.0+, .NET 4.0+, .NET Store).

## Examples

Performing a GET (similar to DELETE)...

	Http.Get("http://www.google.com", (Response) => {
		Console.WriteLine(Response.AsString());
	});
	
Performing a POST (similar to PUT)...

	var Values = new Dictionary<string, string>();
	Values.Add("fieldname", "myvalue");
	Http.Post("http://www.example.com", Values, (Response) => {
		Console.WriteLine(Response.AsString());
	});

Manipulating a request with middleware...

	Http.Get("http://www.google.com", (Response) => {
		Console.WriteLine(Response.AsString());
	}, (Request, Next) => {
		Request.Set("X-Requested-By", "TinyHTTP");
		Next();
	});
