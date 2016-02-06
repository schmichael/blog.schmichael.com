---
title: jQuery Plug-ins for Checkboxes and Disabling Inputs
author: Michael Schurter
layout: post
date: 2009-07-14
url: /2009/07/14/jquery-checkboxes-and-inputs/
dsq_thread_id:
  - 463870918
categories:
  - Open Source
  - Technology

---
Here are 3 helper jQuery functions from my ever-mutating util.js file.

`jQuery.check(<boolean>);` &#8211; Checks or unchecks a checkbox input field based on the boolean you pass it. Very simple, but a handy shortcut. Does _not_ trigger any events like `click` or `change` _by design._

`jQuery.enable()`/`jQuery.disable()` &#8211; Does 3 things:

  1. Adds or removes the &#8220;disabled&#8221; class on all matched elements.
  2. Sets the disabled HTML DOM property on elements which support it (input and select).
  3. Adds or removes the &#8220;disabled&#8221; class for any labels whose `for` attribute matches the ID of an affected `input`.

That last little side effect is what makes these 2 helper functions so handy. I like to subtly theme `label.disabled` to indicate when a field is disabled.

<pre lang="javascript">(function(){
	jQuery.fn.extend({
		check: function(on) { return this.each(function() {
			this.checked = true ? on !== false : false;
		});},
		enable: function() {
			this.removeClass('disabled');
			return this.each(function() {
				if (this.disabled !== undefined) {
					// Only disable elements that support it
					this.disabled = false;

					// Affect labels as well
					$("label[for="+this.id+"]").removeClass("disabled");
				}
			});
		},
		disable: function() {
			this.addClass('disabled');
			return this.each(function() {
				if (this.disabled !== undefined) {
					// Only disable elements that support it
					this.disabled = true;

					// Affect labels as well
					$("label[for="+this.id+"]").addClass("disabled");
				}
			});
		}
	});
})();
</pre>

Would love to hear feedback.