## Co chcemy ustandaryzować?

### Komunikaty

Elektroniczna wymiana dokumentów opiera się o komunikaty. Na początek chcielibyśmy ustandaryzować sześć z nich:


STOCK ENQUIRY
  : Komunikat z żądaniem dostarczenia informacji o cenie (dla danego odbiorcy) i dostępności produktów

STOCK RESPONSE
  : Komunikat z informacją o dostępnych produktach i ich cenie dla żądającego

ORDER
  : komunikat wysyłany przez zamawiającego towar. Oprócz listy zamawianych produktów może zawierać dodatkowe informacje (dostawa/promocja z której korzysta zamawiający)

ORDER RESPONSE 
  : (komunikat nieobowiązkowy) - potwierdzenie przyjęcia zamówienia przez sprzedawcę. Na tym etapie sprzedawca może określić, 
    które produkty zostały skreślone z zamówienia (np. niedostępne w magazynie).

DESPATCH ADVICE 
  : (komunikat nieobowiązkowy) - informacja o wysyłce wraz ze szczegółową informacją o stopniu realizacji zamówienia (w stosunku do poprzedniego 
    komunikatu mogły nastąpić zmiany - na przykład wybrany tytuł nie został znaleziony w magazynie lub wszystkie egzemplarze są uszkodzone). 

INVOICE
  : informacja o wystawionej fakturze do zrealizowanego zamówienia.


### Droga wymiany komunikatów

Najbardziej uniwersalnym sposobem wymiany komunikatów jest E-mail. Każda firma musi mieć dwa adresy E-mail: jeden, na który mają być wysyłane komunikaty, drugi, na który będą odsyłane
informacje o błędach podczas przetwarzania komunikatów (ta skrzynka powinna być regularnie czytana przez wyznaczonego pracownika). 

Komunikat musi być załącznikiem do wiadomości tekstowej, jego typ powinien wskazywać na to, że jest to xml.
