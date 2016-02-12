# Concepts

## Boostrapping
Getting RamenJS installed into your application requires
two bits of code.

```html
<script>
  window.ramenSettings = {
    organization_id: "lkadjf89383hr89",
    user: {
      id: "903849h",
      name: "Bugs Bunny",
      email: "ryan+bugs@ramen.is"
    }
  };
</script>

<script src="https://cdn.ramen.is/assets/ramen.js" async></script>
```
First, you need to define the `window.ramenSettings`
object. 

Then, you need to include the RamenJS library.

The order of operations is important here.
`window.ramenSettings` must be defined before RamenJS
is loaded.

## Custom installation

```html
<script src="https://cdn.ramen.is/assets/ramen.js" async></script>

<!-- Later... -->

<script>
  $(function() { // See note
    Ramen.init.update({
      organization_id: "lkadjf89383hr89",
      user: {
        id: "903849h",
        name: "Bugs Bunny",
        email: "ryan+bugs@ramen.is"
      }
    });
  });
</script>
```

For some more complicated apps, you may not want to,
or be able to, define `ramenSettings` at the time the
page renders.

In that case, load the RamenJS script tag as shown.

Later on, you can call `Ramen.init.update` after the
page has completely loaded.

### A note on order of operations

Note that calls to anything under the `Ramen` object
need to be wrapped in some sort of `onReady` callback

This is an issue we'll be addressing
with RamenJS v2.0, which will ship in the first half
of 2016.

## Secure Mode

Secure Mode ensures that nobody can spoof being one
of your customers. It is disabled by default, because
it takes a little extra developer time to setup
correcgtly.

To enable secure mode, you need to add a few things
to your `ramenSettings` object:

* `timestamp`: The current time in epoch seconds
* `auth_hash`: A SHA-256 hash

### Timestamp

```ruby
ts = Time.now.to_i
```

```javascript
ts = Math.floor(new Date()) / 1000)
```

The `timestamp` attribute must be a time within the last
15 minutes.

### Calculating `auth_hash`

```ruby
array = []
array << "ryan@ramen.is"
array << 42
array << "Ryan Angilly"
array << 1234567890
array << "oihs9uhasdg8934y8"
str = array.join(":")
digest = (Digest::SHA256.new << str).to_s
digest #=> "09cc0a69233f1bf41e68ed00b9256fde5a4542e9fdba635fe2a9a4edf9ee1ba1"
```

The hash is calculated as follows:

1. Create an array with the following elements:
  * `email`: eg. `"ryan@ramen.is"`
  * `id`: eg. `42`
  * `name`: eg. `Ryan Angilly`
  * `timestamp`: eg. `1234567890`
  * `ORGANIZATION_SECRET_KEY`:  eg. `oihs9uhasdg8934y8`

2. Your array now looks like this:
`["ryan@ramen.is", 42, "Ryan Angilly", 1234567890, "oihs9uhasdg8934y8"`

3. Join the elements of that array together with a
colon (`:`) into a string

4. Your string is now: `"ryan@ramen.is:42:Ryan Angilly:1234567890:oihs9uhasdg8934y8"`

5. Generate a SHA256 hash from that string

6. The SHA256 hash for the string in step 4 is:
`09cc0a69233f1bf41e68ed00b9256fde5a4542e9fdba635fe2a9a4edf9ee1ba1`

