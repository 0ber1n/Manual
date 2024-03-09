////////////////////////////////////////////////////

To change the User-Agent of your requests:
1. Go to 'Proxy>Options>Match and Replace'
2. Click 'Add'
3. Change Match to  '^User-Agent.*$' 
1. Change Replage to 'User-Agent: 'Whatever you want to'

////////////////////////////////////////////////////
~To change HTML tags to during intercept, you can enable 'Intercept Reponse' under (Proxy>Settings). From here make sure to enable the proxies and do a full page refresh by hitting:

ctrl + shift + R

~ from here you can forward request until page is loaded and enter new type of values.
~this is usefull to change a field input type from say 'numbers' to 'text'. Then you can utilize that field for commang injection attack.

Example command injections that could be used in a form field is:

$ ;ls;

