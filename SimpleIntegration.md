[Simple Transaction Tracking](#stt)

# Simple Conversion Tracking Integration

## Overview

This document provides technical specifications for advertisers integrating transaction tracking with CJ using the simple iframe version of CJ's tracking tag.

Advertisers must work with a CJ Client Integration Engineer (CIE) to make any integration changes. Advertisers can contact Client Support or submit a request through the Support Center to be assigned a CIE. This document is meant to serve as a guide and must be accompanied by documentation provided by a CIE that contains details specific to the advertiser's account.

All integration changes must be tested along with a CIE before being pushed live, to avoid any breakages in tracking.

### How CJ's Browser-Based Tracking Works

Advertisers send transaction data is to CJ using a browser-based tracking tag. The tracking tags are only fired on the website's transaction confirmation page(s).

When a user clicks on a CJ link, a cookie is created in the browser if a CJ cookie does not already exist. This cookie is assigned a surfer ID that persists in the user's browser. When the advertiser displays the tracking tag, CJ reads the surfer ID and looks for clicks and impressions for that user.

If CJ can find clicks or impressions for that user, then those are correlated to the transaction using Program Terms set up by the advertiser.

## Actions


Actions are advertiser-defined behavior a customer must complete in order for a publisher to receive a commission. Actions can be either leads or sales, and can be sent using simple or advanced data. Your CJ team will help you determine with options are best for you.

### <a href="#stt" /> Simple Transaction Tracking

Simple tracking requires the advertiser to send basic information about a transaction, like an order ID and order subtotal. This method works well when the advertiser does not want to track item-level data about a purchase or lead.

### Advanced Transaction Tracking

Advanced tracking requires the advertiser to send item-level information about a purchase or lead. This method allows for product-level reporting and item-level commissioning.

## Integration Options

CJ recommends that every advertiser integrates with an unconditional CJ tracking tag that fires for all transactions on their website. CJ recommends this method because it gives the advertiser access to Cross-Device Tracking and more robust reporting. If the advertiser chooses conditionally fire their conversion tag, they cannot access Cross-Device Tracking.

### Custom Parameters

CJ can pass URL parameters to the advertiser's website in the query string when a user clicks a CJ link. Advertisers can choose what name=value pairs they want passed. CJ has some standard values that can be passed, like the publisher website ID (PID or CJPID) and the link ID (AID or CJAID). Advertisers can also have custom name=value pairs to indicate, for example, that a user came from CJ (i.e. ref=cj or source=aff).

### Cookie Requirements for Conditional Tags


If the advertiser chooses to apply conditional logic to their CJ tags, it is the advertiser’s responsibility to create their own cookie to track visitors who leave and return, in order to recognize that the visitor was initially CJ- referred and activate CJ-related tracking.

  * Last-click attribution must be used: the last network to send the visitor gets credit for the transaction
  * The cookie must be active for the Program Term's action referral period or longer, with a minimum of 24
hours
  * The user should also get credit for the same amount of occurrences as outlined in the Program Terms. This can vary from one occurrence to unlimited occurrences

## Integrating the Conversion Tag

The conversion tag resides in the HTML body of your Thank You, confirmation, and/or receipt page, which displays following the valid sale or lead process. This page displays the final ordering information, including the order ID, the sale amount, and/or items sold.

Your system must pass our script two vital pieces of information:

  * The unique identifier (OID) specifically captured or generated during the order process
  * The order subtotal before taxes and shipping

The remaining parameters within the conversion tag are static and can be hard-coded into the URL call for that IFRAME
(see the table on the next page). You may place the conversion tag within any dynamic programming language.

<aside class="notice">Important: Use one tag on a confirmation page. Using multiple integration tags on one page interferes with performance.</aside>

## Tag Parameter Summary

+------------+-----------------------------------------------------------------+
| PARAMETER  | REQUIRED / OPTIONAL                                             |
+:===========+:================================================================+
| CID        | REQUIRED                                                        |
+------------+-----------------------------------------------------------------+
| OID        | REQUIRED                                                        |
+------------+-----------------------------------------------------------------+
| TYPE       | REQUIRED                                                        |
+------------+-----------------------------------------------------------------+
| CURRENCY   | REQUIRED                                                        |
+------------+-----------------------------------------------------------------+
| AMOUNT     | REQUIRED                                                        |
+------------+-----------------------------------------------------------------+
| DISCOUNT   | OPTIONAL - SEE NOTES BELOW                                      |
+------------+-----------------------------------------------------------------+
| COUPON     | OPTIONAL - SEE NOTES BELOW                                      |
+------------+-----------------------------------------------------------------+
| CHANNEL    | OPTIONAL - not to be used unless instructed by a CJ team member |
+------------+-----------------------------------------------------------------+
| CHANNEL_TS | OPTIONAL - not to be used unless instructed by a CJ team member |
+------------+-----------------------------------------------------------------+

## Conversion Tag Parameters

<aside class="notice">Note: Parameters are not case-sensitive.</aside>

+-------+---+---------------+-----------------------------------------+
| PARAM | R | EXAMPLE       | NOTES                                   |
| ETER  | E |               |                                         |
|       | Q |               |                                         |
|       | U |               |                                         |
|       | I |               |                                         |
|       | R |               |                                         |
|       | E |               |                                         |
|       | D |               |                                         |
+:======+:==+:==============+:========================================+
| CID   | Y | CID=123456    | This value is set to the Enterprise ID, |
|       | E |               | which is a static value provided by CJ. |
|       | S |               |                                         |
+-------+---+---------------+-----------------------------------------+
| OID   | Y | OID=145\_683- | The OID is a unique identifier, such as |
|       | E | ABC           | an order identifier or invoice number,  |
|       | S |               | which must be populated for each order. |
|       |   |               | It is used to reconcile orders in the   |
|       |   |               | advertiser's system with CJ in order to |
|       |   |               | validate each sale or lead.             |
|       |   |               |                                         |
|       |   |               | -   This value will be truncated after  |
|       |   |               |     the 96th character                  |
|       |   |               | -   Only alphanumeric characters,       |
|       |   |               |     dashes, and underscores can be      |
|       |   |               |     included in the OID field           |
|       |   |               | -   CJ prohibits the submission of      |
|       |   |               |     personally identifiable information |
|       |   |               |     in the OID field, such as a full or |
|       |   |               |     partial email address               |
+-------+---+---------------+-----------------------------------------+
| TYPE  | Y | TYPE=5634     | This is a static value provided by CJ;  |
|       | E |               | it is also called an Action ID in the   |
|       | S |               | Account Manager. Each account may have  |
|       |   |               | multiple actions and each will be       |
|       |   |               | referenced by a different TYPE value.   |
+-------+---+---------------+-----------------------------------------+
| AMOUN | Y | AMOUNT=87.49  | The system assumes the AMOUNT= value is |
| T     | E |               | in the currency specified in the        |
|       | S |               | CURRENCY parameter. If you specify a    |
|       |   |               | currency other than your functional     |
|       |   |               | currency, the system converts the       |
|       |   |               | AMOUNT= value to an amount in your      |
|       |   |               | functional currency using a current     |
|       |   |               | conversion rate.                        |
|       |   |               |                                         |
|       |   |               | The amount value should not include     |
|       |   |               | shipping or tax.                        |
+-------+---+---------------+-----------------------------------------+
| DISCO | N | DISCOUNT=12.9 | Discount parameter which enables you to |
| UNT   | O | 9             | apply a whole order discount to a       |
|       |   |               | transaction.                            |
|       |   |               |                                         |
|       |   |               | An order which contain multiple items   |
|       |   |               | distributes the DISCOUNT value          |
|       |   |               | throughout the items, based on the item |
|       |   |               | amounts.                                |
+-------+---+---------------+-----------------------------------------+
| CURRE | Y | CURRENCY=USD  | Identifies the currency used to         |
| NCY   | E |               | determine the AMT value for each item   |
|       | S |               | involved in the action. This            |
|       |   |               | three-letter code is static and can be  |
|       |   |               | hard-coded into the URL call for the    |
|       |   |               | image.                                  |
|       |   |               |                                         |
|       |   |               | If a code is not specified, product     |
|       |   |               | prices display in the advertiser’s      |
|       |   |               | functional currency. If a blank value   |
|       |   |               | is submitted (“CURRENCY=”, with no      |
|       |   |               | specified value), a transaction error   |
|       |   |               | will occur.                             |
|       |   |               |                                         |
|       |   |               | For a list of supported currencies and  |
|       |   |               | codes, please visit the Support Center. |
+-------+---+---------------+-----------------------------------------+
| COUPO | N | COUPON=10off1 | Parameter for a coupon, voucher or      |
| N     | O | 00            | discount code applied at the time of    |
|       |   |               | purchase.                               |
+-------+---+---------------+-----------------------------------------+
| CONTA | Y |               | The unique identifier for the           |
| INER  | E |               | conversion tag.                         |
| TAG   | S |               |                                         |
| ID    |   |               |                                         |
+-------+---+---------------+-----------------------------------------+
| NAME  | Y |               | If you have multiple conversion tags,   |
|       | E |               | you can use this parameter to uniquely  |
|       | S |               | identify your tags.                     |
+-------+---+---------------+-----------------------------------------+
| CHANN | N |               | *Only use this parameter if instructed  |
| EL    | O |               | by your assigned CJ Client Integration  |
|       |   |               | Engineer*                               |
|       |   |               |                                         |
|       |   |               | This parameter is where the advertiser  |
|       |   |               | passes the channel to which they        |
|       |   |               | attribute the last click.               |
|       |   |               |                                         |
|       |   |               | See the table below for acceptable      |
|       |   |               | values and their meanings.              |
+-------+---+---------------+-----------------------------------------+
| CHANN | N | CHANNEL\_TS=2 | *Only use this parameter if instructed  |
| EL\_T | O | 017-02-14T22: | by your assigned CJ Client Integration  |
| S     |   | 16:46.623Z    | Engineer*                               |
|       |   |               |                                         |
|       |   |               | This parameter is where the advertiser  |
|       |   |               | passes the date/time stamp for the last |
|       |   |               | click that they are attributing the     |
|       |   |               | transaction to. They must use this      |
|       |   |               | format: NOTES: \* format:               |
|       |   |               | yyyy-mm-ddThh24:mm:ss.sssZ \* all dates |
|       |   |               | and times must be in UTC \* the         |
|       |   |               | .toISOString() method in javaScript to  |
|       |   |               | produces this format \* this is the     |
|       |   |               | only format CJ's system will accept     |
+-------+---+---------------+-----------------------------------------+




### Channel Parameter Values

+------------+-------------+------------------------------------------+
| CHANNEL    | ELIGIBLE    | WHEN TO USE IT                           |
| PARAMETER  | FOR CJ      |                                          |
| VALUE      | COMMISSION  |                                          |
+:===========+:============+:=========================================+
| CJ         | YES         | When the customer's last click was from  |
|            |             | a CJ affiliate link                      |
+------------+-------------+------------------------------------------+
| DIRECT     | YES         | When the customer navigated directly to  |
|            |             | the advertiser's website                 |
|            |             |                                          |
|            |             | <aside class="notice">                   |
|            |             | Important: Do not overwrite other        |
|            |             | channels with 'direct'. If there is a    |
|            |             | click for another marketing channel      |
|            |             | before a user navigates directly to the  |
|            |             | site, the 'channel' parameter must       |
|            |             | reflect that previous click.             |
|            |             | </aside>                                 |
+------------+-------------+------------------------------------------+
| AFFILIATE\ | NO          | When the customer's last click was from  |
| _OTHER     |             | an affiliate channel other than CJ       |
+------------+-------------+------------------------------------------+
| DISPLAY    | NO          | When the customer's last click was from  |
|            |             | a display campaign                       |
+------------+-------------+------------------------------------------+
| SOCIAL     | NO          | When the customer's last click was from  |
|            |             | a social media campaign                  |
+------------+-------------+------------------------------------------+
| SEARCH     | NO          | When the customer's last click was from  |
|            |             | a search campaign                        |
+------------+-------------+------------------------------------------+
| EMAIL      | NO          | When the customer's last click was from  |
|            |             | an email campaign                        |
+------------+-------------+------------------------------------------+
| OTHER      | NO          | When the customer's last click was from  |
|            |             | a campaign not defined by the values     |
|            |             | above                                    |
+------------+-------------+------------------------------------------+

NOTE:

  - CJ will consider a transaction eligible for commission in the following scenarios:
    - channel=cj
    - channel=direct
    - channel=[unrecognized value]
    - channel= [blank]
    - channel does not exist in tag  
  - The parameter name and values are not case sensitive
  - If 'direct' is not included as a 'channel' value, the advertiser is not eligible for cross-
device tracking

### Conversion Tag Examples


The following are examples of the conversion tag for simple conversion tracking integration. These coding examples are provided as a courtesy and for your reference only. These examples may not work for your specific shopping cart or web site. CJ does not guarantee the accuracy of these coding examples.

Remember that the tracking tag should be placed within the HTML body of the order’s Thank You, confirmation, and/or receipt page following the order or application process. The AMOUNT and OID variables are populated after submission of the action.

Placeholders with brackets denote the location of required values. Brackets are for illustration purposes only, and should NOT be placed in the actual code. In the example, the TYPE value is paired with a CJ-assigned Action ID number, which identifies the action that has occurred.

Once the conversion tag has been configured to dynamically place the transaction information needed by CJ to process orders, place the final version of the conversion tag within the HTML body of the advertiser’s order confirmation page. Place the conversion tag near the top of the page within the opening and closing body \<BODY\> tags with no visible line breaks. At this point, Technical Services will verify action integration to ensure the placement of the correct data.

#### Simple Conversion Tracking Integration HTML Example

```HTML
<!-- BEGIN CJ TRACKING CODE – DO NOT MODIFY -->
<iframe height="1" width="1" frameborder="0" scrolling="no" src="https://www.emjcd.com/tags/c?containerTagId=<CONTAINERID>& AMOUNT=<AMOUNT>&CID=<ENTERPRISEID>&OID=<OID>&TYPE=<ACTIONID>&CURRENCY=<CURRENCY>" name=Conversion tag> </iframe>
<!-- END CJ TRACKING CODE -->
```

#### Simple Conversion Tracking Integration JavaScript Example

```HTML
<!-- BEGIN CJ TRACKING CODE - DO NOT MODIFY --> <script type="text/javascript">
document.write('< iframe height="1" width="1" frameborder="0" scrolling="no" src="https://www.emjcd.com/tags/c?containerTagId=<CONTAINERID>&AMOUNT='+
[Order[3]] +'&CID=<ENTERPRISEID>&OID=' + [Order[0]] +'&TYPE=<ACTIONID>&CURRENCY=<CURRENCY>" name="cj_conversion"></iframe>');
</script>
<!-- END CJ TRACKING CODE -->
```

#### Simple Conversion Tracking Integration ASP Example

```HTML
<% Username = Request.Form("Username") Password = Request.Form("password") Contact_Name = Request.Form("Contact_Name") Phone = Request.Form("Phone")
Credit_Card = Request.Form("Credit_Card") Address = Request.Form("address") Hosting_Plan = Request.Form("Subtotal")
Card_Number = Request.Form("Card_Number") Expiration = Request.Form("Expiration") Name_On_Card = Request.Form("Name_On_Card")
%> Thank you, <% = Contact_Name %> for your order.</center><br></td></tr> <tr><td>Hosting Plan: <td><% = Subtotal %><br></td><tr> <tr><td><p>Username: <td><% = Username %><br></td></tr> <tr><td>Password: <td><% = Password %></td></tr></table><br> <p>
<!-- BEGIN CJ TRACKING CODE - DO NOT MODIFY -->
<iframe height="1" width="1" frameborder="0" scrolling="no" src="https://www.emjcd.com/tags/c?containerTagId=<CONTAINERID>&CID=<ENTERPRISEID>&OID=<OID>&TYPE =<ACTIONID>&AMOUNT=<AMOUNT>&DISCOUNT=<DISCOUNT>&CURRENCY=<CURRENCY>" name=Conversion tag></iframe></font></td>
<!--END CJ TRACKING CODE.-->
```
