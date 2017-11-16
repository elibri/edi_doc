## Komunikaty


### STOCK ENQUIRY

### STOCK RESPONSE

### ORDER

Zamówienie na produkty. Zamówienie jest realizowane tylko raz, to znaczy, że produkty niedostępne w momencie realizacji zamówienia nie będą później dosyłane. 
Jeśli zamawiane produkty staną się dostępne w późniejszym terminie, muszą zostać ponownie zamówione.

~~~

<?xml version="1.0" encoding="utf-8"?>
<message>
  <kind>ORDER</kind>
  <buyer_number>SK/18777/2017</buyer_number>
  <buyer>SUPERSKLEP</buyer>
  <seller>WYDAWNICTWO-DOBRE-KSIAZKI</seller>
  <delivery>SUPERSKLEP-M1</delivery>
  <order_date>2017-11-19</order_date>
  <line_items>
    <line_item>
      <quantity>2</quantity>
      <ean>9788388722639</ean>
      <buyer_code>SK101</buyer_code>
      <description>Pamięć miłości</description>
      <position>1</position>
    </line_item>
    <line_item>
      <quantity>3</quantity>
      <ean>9788388722684</ean>
      <buyer_code>SK102</buyer_code>
      <description>Dziedzictwo ziemi</description>
      <position>2</position>
    </line_item>
  </line_items>
</message>
~~~

kind:
  : w komunikacie zamówienia zawsze przyjmuje wartość **ORDER**. *Pole wymagane*

buyer_number:
  : numer zamówienia w systemie zamawiającego. *Pole wymagane*.

buyer:
  : kod zamawiającego. *Pole wymagane*.

seller:
  : kod sprzedawcy. *Pole wymagane*.

delivery:
  : kod miejsca dostawy. W przypadku braku tego pola przyjmowana jest wartość z pola buyer

order_date:
  : data złożenia zamówienia

line_items:
  : linie zamówienia. Każda linia jest zawarta w tagu `<line_item>`

line_item.quantity:
  : ilość zamawianego produktu. *Pole wymagane*.

line_item.ean:
  : EAN zamawianiego produktu. *Pole wymagane*.

line_item.buyer_code:
  : kod zamawiającego

line_item.description:
  : nazwa towaru

line_item.position: 
  : numer linii. *Pole wymagane*.

### ORDER RESPONSE

### DESPATCH ADVICE

### INVOICE

