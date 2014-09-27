GoogleCloudUtils.jl
===================

A simple set of utilities for working Google Cloud in Julia. Currently there are only two methods designed to get oauth service account tokens for use in HTTPS requests.

Below is a simple example using `gcloud_authorization()` to get an access token and use it to place a file into Google Cloud Storage.

```julia
using Requests
using JSON

# save a text file to cloud storage
post("https://www.googleapis.com/upload/storage/v1/b/your-bucket-name-here/o",
    data = "Hello, world.",
    headers = {
		"Content-Type" => "text/plain",
		"Authorization" => gcloud_authorization(ENV["HOME"]*"/.ssh/gckey.json")
	},
    query = {"uploadType" => "media", "name" => "example.txt"}
)
```
