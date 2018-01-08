## HATEOAS
> Notes taken from [here](https://spring.io/understanding/HATEOAS) and [here](https://stackoverflow.com/a/13686175/3958178).

In general, a HATEOAS response looks like this:
```
{
	"name": "Alice",
	"links": [
		{
			"rel": "self",
			"href": "http://localhost:8080/customer/1"
		}
	]
}
```

According to the [Richardson Maturity Model](http://martinfowler.com/articles/richardsonMaturityModel.html), HATEOAS is considered the final level of REST. This means that each link is presumed to implement the standard REST verbs of GET, POST, PUT, and DELETE (or a subset). Thus providing the links as shown above gives the client the information they need to navigate the service.

### Relations
- `rel` means relationship. In the above example, it's a self-referencing hyperlink. More complex systems might include other relationships. For example, an order might have a `"rel": "customer"` relationship, linking an order to its customer.
- `href` is a complete URI that uniquely defines the resource.

#### Common Relations
- `self` is the URI that was used to retrieve the current response.
- `start` points back to the API start point.
- `item` points from a collection to an item (e.g. from a Twitter user page to a tweet).
- `collection` is the reverse of `item`.

#### Pagination Relations
> These potentially go against the [Google JSON Style Guide](https://google.github.io/styleguide/jsoncstyleguide.xml#Reserved_Property_Names_for_Links).

- `previous`
- `next`
- `first`
- `last`
