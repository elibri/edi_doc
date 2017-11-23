## Komunikaty


### STOCK ENQUIRY

Jest to żądanie otrzymania informacji o dostępnościach produktów wraz z cenami.

<include filename="stock_enquiry.xml"/>

kind:
  : typ wiadomości, zawsze **STOCK_ENQUIRY**, *pole wymagane*

buyer:
  : identyfikator strony zamawiającej, *pole wymagane*.

seller:
  : identyfikator sprzedawcy, *pole wymagane*.


### STOCK RESPONSE

Jest to odpowiedź na żądanie informacji o dostępnych do sprzedaży produktach i ich cenach (opcjonalnie)

<include filename="stock_response.xml"/>

kind:
  : w tym komunikacie zawsze przyjmuje wartość **STOCK_RESPONSE**, *pole wymagane*

buyer:
  : identyfikator strony zamawiającej, *pole wymagane*.

seller:
  : identyfikator sprzedawcy, *pole wymagane*.

response_date:
  : data wygenerowania cennika, w formacie rrrr-mm-dd, *pole wymagane*

line_items:
  : zawiera zero lub więcej elementów `<line_item>`. Jeśli sprzedający nie współpracuje z kontrahentem, albo odmawia wygenerowania cennika, to powinien
    wygenerować pusty tag `<line_items/>`

    line_item: 
      : linia zamówienia

        ean:
          : EAN produktu, *pole wymagane*

        description:
          : nazwa produktu

        stock_quantity:
          : przybliżona ilość dostępna od ręki do sprzedaży, *pole wymagane*

        expected_ship_date:
          : data pierwszego dnia (w formacie rrrr-mm-dd), w którym będą realizowane zamówienia na ten produkt. 
            W ten sposób można zasygnalizować, kiedy książka będzie dostępna do sprzedaży. 
            Gdy jest podana ta data, to w polu `<stock_quantity>` proszę podawać 0.

        consumer_on_sale_date:
          : w tym polu można podać datę, od kiedy książka może być sprzedawana klientom końcowym, w formacie rrrr-mm-dd.

        retail_price_including_tax:
          : w tym polu można podać cenę detaliczną produktu z podatkiem VAT.

        tax:
          : stawka podatku VAT, w postaci liczby (bez znaku %)

        trade_prices:
          : informacja o cenach sprzedaży produktu dla kontrahenta określonego w tagu `<buyer>`. Cena może zostać powtórzona kilka razy z różną minimalną ilością zakupu produktu.

            trade_price: 
              : block informujący o cenie sprzedaży 

                trade_net_price:
                  : cena netto zakupu produktu

                minimal_amount:
                  : minimalna ilość, którą trzeba zamówić. Brak tego taga oznacza, że minimalna ilość, którą trzeba zamówić to 1 szt./egz.


### ORDER

Zamówienie na produkty. Zamówienie jest realizowane tylko raz, to znaczy, że produkty niedostępne w momencie realizacji zamówienia nie będą później dosyłane. 
Jeśli zamawiane produkty staną się dostępne w późniejszym terminie, muszą zostać ponownie zamówione.

<include filename="order.xml"/>

kind:
  : w komunikacie zamówienia zawsze przyjmuje wartość **ORDER**, *pole wymagane*

buyer_order_number:
  : numer zamówienia w systemie zamawiającego, *pole wymagane*.

buyer:
  : identyfikator zamawiającego, *pole wymagane*.

seller:
  : identyfikator sprzedawcy, *pole wymagane*.

delivery:
  : identyfikator miejsca dostawy. W przypadku braku tego pola przyjmowana jest wartość z pola buyer

order_date:
  : data złożenia zamówienia, w formacie rrrr-mm-dd

line_items:
  : linie zamówienia.

    line_item:
      : linia zamówienia

        quantity:
          : ilość zamawianego produktu, *pole wymagane*.

        ean:
          : EAN zamawianiego produktu, *pole wymagane*.

        description:
          : nazwa towaru

### ORDER RESPONSE

Jest to odpowiedż na zamówienie (nie można odpowiadać jednocześnie na kilka zamówień w jednym komunikacie *ORDER RESPONSE*). W odpowiedzi powinna znaleźć się informacja o pozycjach,
które sprzedawca ma zamiar zrealizować (o części z góry wiadomo, że nie są dostępne). Jeśli sprzedawca odmawia realizacji zamówienia, to powinien wysłać komunikat tylko z nagłówkiem,
bez żadnego produktu.

<include filename="order_response.xml"/>

Są tu powtórzone pola z komunikatu *ORDER*, z wyjątkiem:

kind:
  : rodzaj wiadomości, przyjmuje wartość **ORDER_RESPONSE**

order_buyer_number:
  : identyfikator wiążący ten dokument z oryginalnym zamówieniem, *pole wymagane*

seller_order_number:
  : jest to numer zamówienia w systemie sprzedającego, *pole wymagane*

line_items:
  : line_item:
      : Pola związane z ceną zakupu nie są obowiązkowe, ale bardzo polecamy podawanie tych wartości

        quantity: 
          : musi być większa od zera. Jeśli wybrana pozycja nie może być zrealizowana, powinna zostać usunięta z dokumentu.

        net_price:
          : cena sprzedaży jednostkowa netto.

        net_amount:
          : suma netto

        tax_rate:
          : stawka VAT

        tax_amount:
          : wartość VAT


### DESPATCH ADVICE

Jest to informacja o wysyłce produktów.

<include filename="despatch_advice.xml"/>

Są tu powtórzone pola z komunikatu *ORDER_RESPONSE*, z wyjątkiem:

kind:
  : rodzaj wiadomości, przyjmuje wartość **DESPATCH_ADVICE**


### INVOICE

Jest to faktura wystawiona za towar. Do jednego zamówienia może zostać wystawiona jedna faktura.

<include filename="invoice.xml"/>

kind:
  : typ wiadomości, zawsze **INVOICE**, *pole wymagane*

invoice_number:
  : numer wystawionej faktury, *pole wymagane*

buyer_order_number:
  : numer zamówienia w systemie zamawiającego, wiąże fakturę z oryginalnym zamówieniem, *pole wymagane*.

seller_order_number:
  : jest to numer zamówienia w systemie sprzedającego, *pole wymagane*

buyer:
  : identyfikator zamawiającego, *pole wymagane*.

seller:
  : identyfikator sprzedawcy, *pole wymagane*.

delivery:
  : identyfikator miejsca dostawy. W przypadku braku tego pola przyjmowana jest wartość z pola buyer

invoice_date:
  : data wystawienia faktury, w formacie rrrr-mm-dd, *pole wymagane*

sales_date:
  : data sprzedaży, w formacie rrrr-mm-dd, *pole wymagane*

payment_due_date:
  : termin płatności, w formacie rrrr-mm-dd, *pole wymagane*

seller_name:
  : nazwa sprzedawcy, *pole wymagane*

seller_address:
  : adres sprzedającego - ulica, *pole wymagane*

seller_city:
  : adres sprzedającego - miasto, *pole wymagane*

seller_post_code:
  : adres sprzedającego - kod pocztowy, *pole wymagane*

seller_tax_id:
  : NIP sprzedającego, *pole wymagane*

buyer_name:
  : nazwa kupującego, *pole wymagane*

buyer_address:
  : adres kupującego - ulica, *pole wymagane*

buyer_city:
  : adres kupującego - miasto, *pole wymagane*

buyer_post_code:
  : adres kupującego, - kod pocztowy, *pole wymagane*

buyer_tax_id:
  : NIP kupującego, *pole wymagane*

delivery_detail_name:
  : nazwa miejsca dostarczenia towaru, *pole wymagane jeśli obecna jest wartość delivery*

delivery_detail_address:
  : adres dostarczenia towaru - ulica, *pole wymagane jeśli obecna jest wartość delivery*

delivery_detail_city:
  : adres dostarczenia towaru - miasto, *pole wymagane jeśli obecna jest wartość delivery*

delivery_detail_post_code:
  : adres dostarczenia towaru - kod pocztowy, *pole wymagane jeśli obecna jest wartość delivery*

pdf:
  : obraz faktury pdf zakodowany w base64

line_items:
  : linie fakturty

    line_item:
      : linia faktury

        quantity:
          : ilość produktu, *pole wymagane*.

        ean:
          : EAN produktu, *pole wymagane*.

        net_price:
          : cena sprzedaży jednostkowa netto, *pole wymagane*

        net_amount:
          : suma netto, *pole wymagane*

        tax_rate:
          : stawka VAT, *pole wymagane*

        tax_amount:
          : wartość VAT, *pole wymagane*

        description:
          : nazwa towaru

summary:
  : podsumowanie dokumentu

    total_lines:
      : liczba pozycji na fakturze, *pole wymagane*

    net_amount:
      : wartość netto faktury, *pole wymagane*

    tax_amount:
      : wartość VAT, *pole wymagane*

    gross_amount:
      : wartość brutto faktury, *pole wymagane*

    tax_rate_summaries:
      : podsumowanie faktury pogrupowane według stawek VAT, *pole wymagane*

        tax_rate_summary:
          : podsumowanie dla jednej stawki podatku VAT. Musi wystąpić przynajmniej raz.

            tax_rate:
              : stawka VAT, *pole wymagane*

            net_amount:
              : wartość netto, *pole wymagane*

            tax_amount:
              : wartość VAT, *pole wymagane*

            gross_amount:
              : wartość brutto dla określonej w polu tax_rate stawki VAT, *pole wymagane*


