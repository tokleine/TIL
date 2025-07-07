# Getting nice endpoint names in Azure API Management for C# APIs
## tl;dr
Use the `<summary>` property for your endpoint names, use the `<remarks>` property for your descriptions in C# APIs!

## Description
I recently added a new API to our teams Azure API Mangement (APIM). The endpoints where displayed properly, but in the Azure Portal, the endpoints were named with the descriptions of what the endpoint does, taken from the `"summary"` property from the openapi.json. My team had been using the `<summary>` property to document our controller endpoints. So far this was not an issue, but in APIM this meant that the long-ish text in the `<summary>` ended up being the endpoints name, which was very bad for readability. We hadn't, so far made use of the `"description"` property of the controller endpoints, this property just got populated with a copy of the summary.

To get nice, short endpoint names I changed our API docs from:
```cs
    /// <summary>
    /// My long description of the endpoints functionality
    /// </summary>
    /// <param name="searchRequest"></param>
    /// <param name="cancellationToken"></param>
    /// <returns></returns>
    [HttpGet]
    [ProducesResponseType(200)]
    [ProducesResponseType(400)]
    [ProducesResponseType(500)]
    public async Task<API.MyEndpoint> Search(....)
    {
        ... execute some code ...
    }
```

to:
```cs
    /// <summary>
    /// MyEndpointName
    /// </summary>
    /// <remarks>
    /// My long description of the endpoints functionality
    /// </remarks>
    /// <param name="searchRequest"></param>
    /// <param name="cancellationToken"></param>
    /// <returns></returns>
    [HttpGet]
    [ProducesResponseType(200)]
    [ProducesResponseType(400)]
    [ProducesResponseType(500)]
    public async Task<API.MyEndpoint> Search(....)
    {
        ... execute some code ...
    }
```

Now the API endpoints have nice readable names in APIM. Problem solved ✨
