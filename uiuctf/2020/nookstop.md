# UIUCTF 2020
## nookstop
_The Nook Stop has been acting up today....._

Writeup by **ranguli**

Challenege by **ian5v**

Visiting the challenge link [https://nookstop.chal.uiuc.tf/](https://nookstop.chal.uiuc.tf/) brings us to a page where the "Flag"
button moves around dodging the mouse before you can click it. You can try using the "Tab" key to
iterate through the elements on the page and hit enter on the flag button but
you'll end up with:

```
Not that easy c: but here's a crumb: uiuctf{w
```

The word crumb here is a hint as we'll see soon. I'm interesting in starting out by looking at the JavaScript on the page to see if there is anything of interest. Viewing the source of the page we see a `cookie.js` file, which contains a helper function for dealing with cookies and a comment complaining about how cookie manipulation isn't a feature in vanilla JS. If it wasn't already clear, "crumb" in the last section was a reference to "cookies".

Next we see some inline JavaScript. Something of interest is the following few
lines of jQuery:

```javascript
	$("#flag").click(function(){
		console.log("TODO: シークレット_バックエンド_サービスを可能にする");
		document.cookie = "clicked_flag_button=true";
		location.reload();
	});
```

This Japanese reads (according to Google Translate), "TODO: Enable Secret_Backend_Service". We see a cookie `clicked_flag_button` being set to `true`, which we can verify exists if we check our cookies in our broser.

At this point I took a guess that we need to manipulate cookies, and it was
probably going to involve adding a new cookie like `secret_backend_service=true`. Sure enough after adding this cookie and refreshing the page, we get the flag.

```
uiuctf{wait_its_all_cookies?}
```

(Always has been)
