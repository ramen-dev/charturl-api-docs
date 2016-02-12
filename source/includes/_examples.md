# Examples

Here are some heavily commented examples.

## Ruby/ERB

If you're on Ruby on Rails, you should check out our [Rubygem](https://rubygems.org/gems/ramen-rails),
but if not, here is a Ruby/ERB example.

```ruby
<!-- 1. OPTIONAL: This <link> tag can goes at the top of your <head> to prefetch DNS -->
<link rel="dns-prefetch" href="http://cdn.ramen.dev">

<!-- 2. This script tag can go anywhere in the <body> but **before** the RamenJS tag -->
<script>
  <% @ts = Time.now.to_i %> <!-- Optional unless you want to use Secure Mode -->
  window.ramenSettings = {
    organization_id: "ORGANIZATION_ID",
    user: {
      // Required. If you don't have a name, pass in their email here.
      name: <%= current_user.name.to_json.html_safe %>,

      // Required. If you don't have email addresses for your logged in users, please contact support@ramen.is
      email: <%= current_user.email.to_json.html_safe %>,

      // Required. This must be unique. Changing this creates a new Customer.
      id: <%= current_user.id.to_s.to_json.html_safe %>,

      // Optional
      created_at: <%= current_user.created_at.to_i %>
    } // If you uncomment the optional attributes below, don't forget to add a comma (",") here

    // The next two keys are optional unless you want to enable Secure Mode
    // timestamp: <%= @ts %>,
    // auth_hash: <%= (Digest::SHA2.new << "#{current_user.email}:#{current_user.id}:#{current_user.name}:#{@ts}:ORGANIZATION_SECRET_KEY").to_s.to_json.html_safe %>
  };
</script>

<!-- 3. This goes just before the closing </body> tag and **always after** where you set window.ramenSettings -->
<script src="http://cdn.ramen.dev/assets/ramen.js" async>
</script>
```

## JavaScript

```html
<!-- 1. OPTIONAL: This <link> tag can goes at the top of your <head> to prefetch DNS -->
<link rel="dns-prefetch" href="https://cdn.ramen.is">

<!-- 2. This script tag can go anywhere in the <body> but **before** the RamenJS tag -->
<script>
  window.ramenSettings = {
    organization_id: "YOUR_ORGANIZATION_ID",
    user: {
      // Required. If you don't have a name, pass in their email here.
      name: "Ryan Angilly",

      // Required. If you don't have email addresses for your logged in users,
      // please contact support@ramen.is
      email: "ryan@ramen.is",

      // Required. This must be unique. Changing this creates a new Customer.
      id: "527de734763a556882001003",

      // Optional
      created_at: 1234567890
    } // If you uncomment the optional attributes below, don't forget to add a comma (",") here

    // The next two keys are optional unless you want to enable Secure Mode
    // timestamp: ts_used_server_side_to_calculate_auth_hash,
    // auth_hash: auth_hash_calculated_server_side
  };
</script>

<!-- 3. This goes just before the closing </body> tag and **always after** where you set window.ramenSettings -->
<script src="https://ramen.is/assets/ramen.js" async>
</script>
```

## Wordpress/PHP

If you're on Wordpress, you should checkout our [Eager.io](#eager-io) integration,
but here is an example:

```html
<!-- 1. OPTIONAL: This <link> tag can goes at the top of your <head> to prefetch DNS -->
<link rel="dns-prefetch" href="http://cdn.ramen.dev">

<!-- 2. This script tag can go anywhere in the <body> but **before** the RamenJS tag -->
<?php if ( is_user_logged_in() ) { ?>

<?php global $current_user;
  get_currentuserinfo();
  $user_roles = $current_user->roles;
  $user_role = array_shift($user_roles);

  // The next two keys are optional unless you want to enable Secure Mode
  $_ramen_ts = time();
  $_ramen_items = array($current_user->user_email, $current_user->ID, $current_user->display_name, $_ramen_ts, "ORGANIZATION_SECRET_KEY");
?>

<script>
  window.ramenSettings = {
    organization_id: "ORGANIZATION_ID",
    user: {
      // Required. If you don't have a name, pass in their email here.
      name: "<?php echo $current_user->display_name; ?>",

      // Required. If you don't have email addresses for your logged in users, please contact support@ramen.is
      email: "<?php echo $current_user->user_email; ?>",

      // Required. This must be unique. Changing this creates a new Customer.
      id: <?php echo $current_user->ID; ?> ,

      // Optional
      created_at: <?php echo $current_user->created_at; ?>
    } // If you uncomment the optional attributes below, don't forget to add a comma (",") here

    // The next two keys are optional unless you want to enable Secure Mode
    // timestamp: <?php echo $_ramen_ts ?>,
    // auth_hash: "<?php echo hash("sha256", implode(":", $_ramen_items)); ?>"
  };
</script>
<?php } ?>


<!-- 3. This goes just before the closing </body> tag and **always after** where you set window.ramenSettings -->
<script src="http://cdn.ramen.dev/assets/ramen.js" async>
</script>
```


## Python

Thanks to fjania for putting this together. Gist available
[here](https://gist.github.com/ryana/41b7de953fb314c00a7a#file-gistfile1-py)

```python
import hashlib
import time

def ramen(request):
    ramen_js = '';
    if not request.user.is_anonymous():
        email = request.user.email
        user_id = request.user.id
        name = "{} {}".format(request.user.first_name, request.user.last_name)
        timestamp = int(time.time())
        secret_key = "SECRET_KEY_GOES_HERE"
        auth_input = "{}:{}:{}:{}:{}".format(
            email,
            user_id,
            name,
            timestamp,
            secret_key,
        )
        auth_hash = hashlib.sha256(auth_input).hexdigest()

        ramen_js = '''
        <!-- This can go anywhere before the ramen.js tag -->
        <script>
            window.ramenSettings = {{
                organization_id: "555cc17077656204242f0000",
                user: {{
                    name: "{name}",
                    email: "{email}",
                    id: "{id}",
                }},
                timestamp: {timestamp},
                auth_hash: "{auth_hash}"
            }};
        </script>
        <!-- This goes before the </body> tag -->
        <script src="https://cdn.ramen.is/assets/ramen.js" async>
        </script>
        '''.format(
            name = name,
            id = user_id,
            email = email,
            timestamp = timestamp,
            auth_hash = auth_hash,
        )

    return { 'ramen_js': ramen_js }
```
