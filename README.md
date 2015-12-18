jquery-pos v0.0.1 _Beta_
========================

Point of sale hardware support plugin for jQuery

I have currently only tested this plugin on 1 type of barcode scanner and credit card magnetc stripe reader. However, so far tests have been very successful and promising.
Any code contributions are much appreciated as I'm sure we can develop more extensive Regexp options that span accross different barcode types and other forms of CC Data.

Here's a blog post containing some basic info and caveats about the plugin: http://www.devlifeline.com/2014/05/using-point-of-sale-hardware-in-cloud.html

#Usage

Simply include _jquery.pos.js_ on your site then use the following code block:
```javascript
$(function(){
	$(document).pos();
	$(document).on('scan.pos.barcode', function(event){
		//access `event.code` - barcode data
	});
	$(document).on('swipe.pos.card', function(event){
		//access following:
		// `event.card_number` - card number only
		// `event.card_holder_first_name` - card holder first name only
		// `event.card_holder_last_name` - card holder last name only
		// `event.card_exp_date_month` - card expiration month - 2 digits
		// `event.card_exp_date_year_2` - card expiration year - 2 digits
		// `event.card_exp_date_year_4` - card expiration year - 4 digits
		// `event.swipe_data` - original swipe data from raw processing or sending to a 3rd party service
	});
});
```

You can also override the following default options...

```javascript
var options = {
    scan: true, //enable scan event
    submit_on_scan: false, //allow the keycode 13 event to continue on scan
    swipe: true, //enable swipe event
    submit_on_swipe: false, //allow the keycode 13 event to continue on swipe
    events: {
        scan: {
            barcode: 'scan.pos.barcode' //event name for successfully scanned barcode
        },
        swipe: {
            card: 'swipe.pos.card' //event name for successfully scanned card
        }
    },
    regexp: {
        scan: {
            barcode: '\\d+' //regexp for barcode validation
        },
        swipe: {
            card: '\\%B(\\d+)\\^(\\w+)\\/(\\w+)\\^\\d+\\?;\\d+=(\\d\\d)(\\d\\d)\\d+\\?' //regexp for credit card validation
        }
    },
    prefix: {
        scan: {
            barcode: '' //prefix for barcode - will be added to regexp
        },
        swipe: {
            card: '' //prefix for credit card - will be added to regexp
        }
    }
};

$(document).pos(options);
```
