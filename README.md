jquery-pos
==========

Point of sale hardware support plugin for jQuery

Simply include _jquery.pos.js_ on your site then use the following code block:
```javsacript
$(function(){
	$(document).pos();
	$(document).on('scan.pos.barcode', function(event){
		//access `event.code` - barcode data
	});
	$(document).on(swipe.pos.card', function(event){
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
