# walmart-orders-csv
Pull walmart order info into a csv using browser developer tools

## Guide

Open up the Walmart Orders
View Walmart Order, Open up accordian if needed

Open up Developer Tools. Ie, right click, select inspect element
Go to Console Tab
Input the following:

```
date = Array.from(document.getElementsByClassName("print-bill-date")).map((v)=>{return v.textContent})[0].replace(" order","").replace(" purchase","")
document.querySelectorAll('div[data-testid=productName]');
items = Array.from(document.querySelectorAll('div[data-testid=productName]')).map((e)=>{
   return e.textContent;
});
document.querySelectorAll('div[class="ml-auto"]')
prices = Array.from(document.querySelectorAll('div[class="ml-auto"]')).map((e)=>{
   return e.firstChild.firstChild.textContent.split("$")[1];
});
rows = items.map((item,i)=>{
    return date+"|"+item+"|"+prices[i]
})
csv = "Date|Item|Price" + "\r\n" + rows.join("\r\n")
console.log(csv)
```
Pipe delimited CSV should be output.

Copy and Paste CSV data to Excel or your choice. Import using "|" delimiter.

## Very Important Note
The selectors and parsing will break *very* easily. Good luck.
