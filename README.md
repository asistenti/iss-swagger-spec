# iss-swagger-spec

Trenutna verzija specifikacije: 1.1.0

# Schemas sekcija na kraju swagger-a samo sadrzi strukture koje su koriscene za izgradnju dokumenta. Nemojte praviti klase poda takvim nazivom, plus nemojte ih kopirati 1 na 1 posto u svakom endpoint-u je dodavan po jos sta od atributa u odnosu na te stavke koje su definisane tamo. Obratiti paznju u svakom endpoint-u na sadrzaj i opis elemenata zahteva i izgled JSON-a koji predstavlja odgovor.

Izmene po verzijama:

1.1.0:

- Dodat prefix ,,/api,, na svaku putanju
- Dodat prevedena kompletna specifikacija na engleski (svi naiziv atributa su sada na engleskom)
- Dodati endpoint-i za recenziju vozila (samim tim dodato i polje liste recenzija kod vozila u modelu)
- Dodat ,,name,, atribut u koordinatama koji ce spreciti potrebu reverse geocoding-a (dodat i u modelu).
- Izbacen pocetak radnog vremena prilikom kreiranja istog jer je to podatak koji se moze generisati na serveru
- Izbacen kraj radnog vremena prilikom azuriranja istog jer je to podatak koji se moze generisati na serveru
- Kod povratnih vrednosti za korisnike, ne vraca se password polje
- Kod poruke kao povratne vrednosti prilikom kreiranja vraca se i senderId
