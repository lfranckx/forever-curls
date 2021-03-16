Order properties
Many properties of an order are available directly using Liquid, in templates, and in additional scripts.

The properties of an order are available in the following templates:

Order confirmation
New order
New order (mobile)
Shipping confirmation
Shipping update
Additional scripts
Fulfillment request
Note
Unlike most other Liquid objects, the order object isn't referenced by name in email templates. For example, instead of using {{ order.shipping_method.title }} in your order confirmation email template, you should use {{ shipping_method.title }}. However, for SMS notifications, order properties need to be prepended with order as usual.

Property	Description
id
A system wide unique ID of the order for internal use. Use the following example to generate a link to the order in the admin section of your shop. For example, in your New order template, you can add the following code:

<a href="{{ shop.url }}/admin/orders/{{ id }}">View order</a>
email
The email associated with the order.
name
Typically this is a pound symbol followed by the order_number.

Example: #1004

order_name
Same as name.
order_number
Shop unique number of the order, without the pound # prefix, or any prefix or suffix added to the order ID by the shop-owner in their shop preferences.

Example: 1004

created_at
The date and time the customer created the order. You can format this using the date filter.

Example: 2009-05-30T17:43:51+02:00

tags	Returns an array of all of the order's tags. The tags are returned in alphabetical order. Please see our Liquid reference documentation for more details.
transactions	Returns an array of transactions from the order.
tax_price
The combined taxes of all the items in the order.
tax_lines
Taxes broken up by type of taxation:

{% for tax_line in tax_lines %}
    {{ tax_line.title }} ({{ tax_line.rate_percentage }}%) : {{ tax_line.price | money_with_currency  }}
{% endfor %}
tax_line.title
The name of the tax.

Examples: QST or VAT

tax_line.price
The amount.
tax_line.rate
The rate. It will return 0.175 if it is 17.5%.
tax_line.rate_percentage
The tax rate in human readable form. It will return 17.5 if the rate is 0.175.
customer
Customer object containing the attributes of the customer output.
billing_address
The billing address.
billing_address.first_name
First name of the customer.
billing_address.last_name
Last name of the customer.
billing_address.company
Company name for billing.
billing_address.phone
Phone number from the billing address.
shop.name
Name of your store.
shop.phone
Your store's phone number.
subtotal_price
Sum of the order's line-item prices after any line-item discount or cart discount has been deducted. The subtotal doesn't include taxes (unless taxes are included in the prices), shipping costs, or tips.
discounts
A list of discounts.
discounts_amount
The amount of the discount applied by all discounts.

Example: +$5.00

discounts_savings
The amount of the savings caused by all discounts.

Example: -$5.00

total_price
Total of the order (subtotal + shipping cost - shipping discount + tax).

financial_status
The current payment status. One of: nil, pending, authorized, paid, voided, refunded.
requires_shipping
(boolean) Returns true if there is at least one item in the order that requires shipping.
shipping_method.title
The Shipping rate name.

Example: Standard Shipping

shipping_method.price
The shipping price including any shipping discount.

Example: {{ shipping_method.price | money }}

shipping_price
The shipping price.

Example: {{ shipping_price | money }}

shipping_address
The shipping address.
shipping_address.first_name
The first name for the shipping address.
shipping_address.company
Company name for shipping address.
shipping_address.phone
Phone number from the shipping address.
line_items
List of all Line Items in the order.
item_count
A sum of all the items' quantities.
fulfillment_status
The current fulfillment status of the order. One of: unfulfilled, partial, fulfilled.
note
The note which is attached to the order. The note can be obtained from the customer and/or edited in the order detail screen in your admin interface.
attributes
Any attributes which were attached to the order.

Example: {{ attributes.gift-note }}

referring_site
Contains the url of the referrer that brought the customer to your store.

Example: https://www.google.com/?s=great+products

landing_site
Contains the path of the landing site the customer used. This is the first page that the customer saw when he/she reached the store.

Example: /products/great-product?ref=my-tracking-token

landing_site_ref
Looks at the landing site and extracts a reference parameter from it. Reference parameters can be: ref, source, r.

If the landing_site is /products/great-product?ref=my-tracking-token, then the landing_site_ref is my-tracking-token. You can perform a certain action if your ref is equal to a certain value:

{% if landing_site_ref == 'my-tracking-token' %}
My action...
{% endif %}
cancelled
(boolean) Returns true if the order has been canceled.
cancelled_at
The time when the order was canceled.
cancel_reason
The reason selected when canceling the order. One of: inventory, customer, declined, fraud, or other.
has_high_risks?
Returns true if the order has high risk

translate="no"
unique_gateways
Returns a list of unique payment providers on an order. For example, if someone paid with a Visa, a Mastercard, and cash, the returned list would be shopify_payments, cash.

location (POS only)
Displays the physical location of the order. There are several location properties available, listed here. You can configure locations in the Locations area of the admin.

order_status_url
Returns the link to the order status page for this order.

fulfilled_line_items
(deprecated)
List of Line Items which have been fulfilled.
unfulfilled_line_items
(deprecated)
List of Line Items which haven't been fully fulfilled.
Draft order properties
Draft order properties are available on the Draft Order Invoice email template, which notifies your customers about outstanding invoices.

Note
You can't send draft order notifications by using SMS.

Property	Description
id
A unique ID of the draft order for internal use.
invoice_url
A link the customer can follow to pay for the invoice using Shopify's secure checkout.
reserve_inventory_until
The date and time the line items in the draft are reserved until, for example, 2015-05-30T17:43:51+02:00.

You can format dates using the Liquid date filter.

user
The last staff member who modified the draft order.
user.name
The name of the last staff member who modified the draft order.
user.email
The email address of the last staff member who modified the draft order.
email
The email address associated with the draft order.
name
The unique number of the draft order, prefixed by a number sign #.
number
The unique number of the draft order without the order prefix or suffix.
created_at
The date and time the customer created the draft order, for example, 2009-05-30T17:43:51+02:00.

You can format dates using the Liquid date filter.

tags	Returns an array of all of the order's tags. The tags are returned in alphabetical order. Please see our Liquid reference documentation for more details.
tax_price
The combined taxes of all the items in the draft order.
tax_lines
Taxes broken up by type of tax:

{% for tax_line in tax_lines %}
{{ tax_line.title }} ({{ tax_line.rate_percentage }}%) : {{ tax_line.price | money_with_currency  }}
{% endfor %}
tax_line.title
The name of the tax.

Examples: QST or VAT

tax_line.price
The tax amount.
tax_line.rate
The tax rate in decimal form. For example, a tax rate of 17.5% will return 0.175.
tax_line.rate_percentage
The tax rate in percentage form. For example, a rate of 0.175 will return 17.5.
customer
Customer object containing the attributes of the customer output.
billing_address
The billing address for the draft order.
billing_address.first_name
The customer's first name.
billing_address.last_name
The customer's last name.
billing_address.company
The company name in the billing address.
billing_address.phone
The phone number in the billing address.
shop.name
The name of your store.
shop.phone
Your store's phone number.
subtotal_price
Sum of the draft order's line-item prices after any line-item discount or cart discount has been deducted. The subtotal doesn't include taxes (unless taxes are included in the prices) or shipping costs.
discounts
A list of discounts.
discounts_amount
Amount of the discount applied by all discounts.

Example: +$5.00

discounts_savings
Amount of the savings caused by all discounts.

Example: -$5.00

total_price
The total price of the order (subtotal + shipping cost - shipping discount + tax).
requires_shipping
Returns true if there is at least one item in the draft order that requires shipping. Returns false if no items in the draft order require shipping.
shipping_method.title
The Shipping rate name.

Example: Standard Shipping

shipping_method.price
The price of the shipping method. Returns the same information as shipping_price.
shipping_price
The shipping price.

You can format this amount using Liquid money filters.

shipping_address
The shipping address.

Note: Unlike in regular orders, a draft order's shipping address may be incomplete.

shipping_address.first_name
The first name for the shipping address.
shipping_address.company
The company name in the shipping address.
shipping_address.phone
The phone number in the shipping address.
line_items
A list of all line items in the draft order.
item_count
A sum of all the item quantities in the draft order.
note
The note attached to the draft order. The note can be obtained from the customer and also edited in the draft order detail screen in your Shopify admin.
location
The physical location of the order. There are several location properties available.

You can configure locations in the Locations page of your Shopify admin.

Line item properties
Each line in the list of line_items or subtotal_line_items has the following properties.

Tip
subtotal_line_items returns the line items that are used to calculate the subtotal_price of an order. subtotal_line_items excludes tip line items.

Property	Description
line.applied_discounts
(POS and draft orders only)
List of discounts applied to this item (each discount has the title, code, amount, savings and type properties).
line.custom
(Draft orders only)
(boolean) Returns true if the item is a custom line item for a draft order.
line.grams
Weight of a single item.
line.image
Returns the URL of the image associated with this line item. You can also use the img_url filter to get specific image sizes, for example {{ line.image | img_url: 'small' }}
line.line_price
The price multiplied by the quantity for that item.
line.original_line_price
The combined price of the quantity of items included in the line, before discounts were applied.
line.final_line_price
The combined price of all the items in the line item, including all line level discount amounts.
line.price
The price for a single item.
line.product.title
The name of the product.
line.product.vendor
The vendor for the item.
line.properties
Returns an array of custom information for an item. Line item properties are specified by the customer on the product page, before adding a product to the cart.
line.quantity
Quantity for that item.
line.requires_shipping
(boolean) Returns true if the variant for the item has the checkbox This is a physical product checked on the product page.
line.selling_plan_allocation
Returns a selling_plan_allocation object, which describes how a selling plan such as a subscription impacts the line item.
line.taxable
(boolean) Returns true if the variant for the item has the checkbox 'Charge taxes on this product' checked on the product page.
line.title
The name of the product followed by a dash followed by the name of the variant. The variant name isn't included when it is “Default Title”.
line.url
The relative URL of the line item's variant. The relative URL doesn't include your store's root URL (mystore.myshopify.com).
line.variant.barcode
The barcode associated with the product variant.
line.variant.compare_at_price
The compare at price associated with the product variant.
line.variant.image
The image for the product variant. Only returns an image if there is a specific image assigned to the variant in the line item.
line.variant.sku
The SKU associated with the product variant.
line.variant.title
The variant's option values, joined by / characters.

Example: small / red

Refunds properties
These additional properties are available on the Refunds email template. This email template is used to notify your customers that a refund (complete or partial) has been applied to their order. You can use any variable available for the Order email notification template, in addition to the following variables:

Property	Description
amount
The amount of money refunded.
refund_line_items
A list of refund line items to be refunded.
Refund_line_item properties
Each refund_line in the list of refund_line_items has the following properties:

Property	Description
refund_line.line_item
The line_item that is being refunded. This has access to all the line_item’s properties.
refund_line.quantity
The quantity of the line item to be refunded.
Fulfillment properties
These additional properties are available on the Shipping confirmation, Shipping update and Fulfillment request email templates.

The Shipping confirmation and Shipping update are used to notify your customers that some or all items in their order have been successfully fulfilled, or updated with new shipping information.

The Fulfillment request email template is used for any custom fulfillment service defined in your shop admin. To add a custom fulfillment service, go to Settings > Shipping and scroll down to Fulfillment/Dropshipping.

Property	Description
service_name
The name of the custom service as defined in the Settings > Shipping page. (Fulfillment request only)
fulfillment.estimated_delivery_at
An estimated delivery date based on the tracking number (if available) provided by one of the following carriers: USPS, FedEx, UPS, Canada Post (Canada only). This property is only available when carrier-calculated rates are in use.
fulfillment.fulfillment_line_items
A list of fulfillment line items to be fulfilled.
fulfillment.item_count
A sum of all the items' quantities. The total number of items being fulfilled.
fulfillment.requires_shipping
(boolean) Returns true if this fulfillment request requires shipping.
fulfillment.tracking_company
The company doing the tracking.
fulfillment.tracking_numbers
A list of tracking numbers.
fulfillment.tracking_urls
A list of tracking URLs.
items_to_fulfill
(deprecated)
A list of line items that are to be fulfilled by this particular custom fulfillment service. (Fulfillment request only)
items_to_fulfill_count
(deprecated)
The total number of items to be fulfilled by this request. (Fulfillment request only)
Fulfillment_line_item properties
Each fulfillment_line in the list of fulfillment_line_items has the following properties.

Property	Description
fulfillment_line.line_item
The line_item being fulfilled. This has access to all the line_item's properties.
fulfillment_line.quantity
The quantity of the line item that is being fulfilled.
Delivery properties
Property	Description
delivery_instructions
Local delivery information to share with the customer. This information is controlled by the Delivery information field in your local delivery settings.
Discount properties
There are two types of discount properties.

discount_applications describe why and how an item was discounted.

discount_allocations describe how a particular discount affects a line item and how it reduces the price. You should use this property at the line item level.

You can combine these properties to display discount information at the line item or order level.

Example
This example checks if a discount has been applied to the line item. If the discount wasn't applied at the order level (all), then the discount name and amount are displayed.

{% if line.discount_allocations %}
    {% for discount_allocation in line.discount_allocations %}
        {% if discount_allocation.discount_application.target_selection != 'all' %}
            {{ discount_allocation.discount_application.title | upcase }}
            (-{{ discount_allocation.amount | money }})
        {% endif %}
    {% endfor %}
{% endif %}
The result might look like this:

SPRING5 (-$5.00)
Discount_allocation properties
Each discount_allocation in the list of discount_allocations has the following properties.

Property	Description
discount_allocation.amount
The amount of money saved by the customer on a line item. Must be entered in a loop if you want to allow multiple discount codes.
discount_allocation.discount_application
The discount application that allocates the amount on the line item.
Discount_application properties
Each discount_application in the list of discount_applications has the following properties.

Property	Description
discount_application.target_selection
Describes how a discount selects line items in the cart to be discounted. One of:

all: The discount applies to all line items.
entitled: The discount applies to a particular subset of line items, often defined by a condition.
explicit: The discount applies to a specifically selected line item or shipping line.
discount_application.target_type
The type of item that a discount applies to (line_item or shipping_line).
discount_application.title
The customer-facing name of the discount.

Examples: Welcome10 or CBBWQQAKYBYY

discount_application.total_allocated_amount
The total amount that the price of an order is reduced by the discount.
discount_application.type
The type of the discount. One of: automatic, discount_code, manual, or script.
discount_application.value
The value of the discount.
discount_application.value_type
The value type of the discount. One of: fixed_amount or percentage.
Email notification properties
Property	Description
shop.email_logo_url
The url for the logo specified in the Customize email templates section of the admin.
shop.email_logo_width
The logo width (pixels) specified in the Customize email templates section of the admin.
shop.email_accent_color
The HEX code for the accent color specified in the Customize email templates section of the admin.