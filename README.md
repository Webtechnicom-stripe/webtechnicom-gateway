# webtechnicom-gateway
payment systems
# webtechnicom-gateway
payment systems
// Include this library using the bootstrap.php file
include_once 'chargedesk-php/bootstrap.php';

// Setup your api key, so we know who you are
ChargeDesk::apiKey("sk_JLKtGQlBCgwmt9vcG0QuiApePtHEoPOb");

// Create a new charge in the system
$charge = ChargeDesk_Charge::create(array(
    "amount" =>     "49.00",
    "currency" =>   "USD",
    "customer" =>   array(
        "id" => "example@chargedesk.com"
    )
));
// $charge now contains the data from the charge you've just created

echo $charge->support_url; // Print out the individual support URL
// Include this library using the bootstrap.php file
include_once 'chargedesk-php/bootstrap.php';

// Setup your api key, so we know who you are
ChargeDesk::apiKey("sk_JLKtGQlBCgwmt9vcG0QuiApePtHEoPOb");

// Example of running a large number of requests
$offset = 0;
while($offset < 40) {
    try {
        $charges = ChargeDesk_Charge::find(array(
            "count" => 1,
            "offset" => $offset,
        ));
        print $offset." - Charge ID: ".$charges->data[0]->charge_id."<br />";
        $offset++;
    }
    catch(ChargeDesk_RateLimitError $e) {
        // Wait for the specified time before trying the request again
        print "<b>Hit rate limit. Sleeping for ".$e->getHeader('Retry-After')." seconds</b><br />";
        sleep($e->getHeader('Retry-After'));
    }
}
