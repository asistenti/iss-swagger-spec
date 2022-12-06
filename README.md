# iss-swagger-spec

Trenutna verzija specifikacije: 1.1.0

# Schemas sekcija na kraju swagger-a samo sadrzi strukture koje su koriscene za izgradnju dokumenta. Nemojte praviti klase pod takvim nazivom, plus nemojte ih kopirati 1 na 1 posto u svakom endpoint-u je dodavano po jos sta od atributa u odnosu na te stavke koje su definisane tamo. Obratiti paznju u svakom endpoint-u na sadrzaj i opis elemenata zahteva i izgled JSON-a koji predstavlja odgovor.

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

1.1.1:

- Dodate lokacije u svaki odgovor koji vraca Ride
- Dobavljanje poruka sada ima query parametar userId, jer se ne dobavljaju sve poruke korisnika, nego sa potrebe chat-a se dobavljaju njegove poruke u kojima je on sender i receiver, ali u vezi sa nekim drugim korisnikom sto predstavlja bas userId
- Dodata su 2 endpoint-a sa dobavljanje trenutne AKTIVNE voznje za vozaca i putnika.

1.1.2:

- Ispravljene su putanje za review. GET /api/review/{driverId} -> GET /api/review/driver/{id}
                                    GET /api/review/{vehicleId} -> GET /api/review/vehicle/{id}

1.1.3:

- Greska kod putanje /api/user/{id}/message. Naveden je pored id-a i userId parametar koji je slucajno ostao neobrisan.
- Greska kod putanje /api/reviews/{rideId} -> /api/review/{rideId} Uklonjeno je ,,s,, za mnozinu.

1.1.4:

- Promenjen naziv atributa ,,departures,, u ,,departure,, u endpoint-u POST /api/ride i POST /api/unregisteredUser/
- Odgovor prilikom kreiranja review-a i za vozača i vozilo ima promenjen atribut sa review u comment.
- Potencijalne enum vrednosti (VOZNJA, VOZAC, Prihvaceno, Zavrseno, Odbijeno) preimenovane u (RIDE, DRIVER, ACCEPTED, FINISHED, REJECTED)

1.1.5:

- Ispravljene semanticke greske koje je swagger prijavljivao. Pogledati sam commit sa razlike.

1.1.6:

- Izbacen tip iz passengers i driver atributa kod voznje jer je redundantan
- Reimenovan atribut poruka u message kod otkazivanja voznje od strane putnika
- U odgovoru za kreiranje panic-a, vracaju se user i ride umesto userId i rideId
- Uklonjen id driver-a iz request body-a kod azuiranja postojeceg driver-a
- driver-id je izbacen iz endpointov-a: GET i PUT /api/driver/{driver-id}/working-hour/{working-hour-id} pa sad ti endoint-ovi su GET i PUT /api/driver/working-hour/{working-hour-id}

1.1.7:

- POST promenjen u GET kod aktivacije naloga
- /api/review/{rideId} sada vraca listu objekata za review vozila i vozaca zbog toga sto vise putnika moze da ostavi ocenu za vozilo i vozaca u istoj voznji
- U svim review endpoint-ovima se dodatno vraca i podatak o putniku koji je ostavio review. Kada se review kreira, to je podatak koji se moze izvuci iz JWT-a, koji cete tek raditi na predavanju, tako da svakako nije neophodno da se salje ko je ostavio review
- Prilikom kreiranja review-a, treba nam i podatak na koji ride se odnosi review, pa je dodat u putanji:
POST /api/review/driver/{id} -> POST /api/review/{rideId}/driver/{id}
POST /api/review/vehicle/{id} -> POST /api/review/{rideId}/vehicle/{id}
- Dodati id, status i odbijenica u svim ride odgovrima. Id i status je nesto ce uvek postojati, a odbijenica ce najcesce imati null vrednost prilikom vracanja
- Ispravljene putanje za aktivne voznje kod vozaca i putnika zbog ambigous greske u Spring-u
/api/ride/active/{driverId} -> /api/ride/driver/{driverId}/active
/api/ride/active/{passengerId} -> /api/ride/passenger/{passengerId}/active
- Locations u odgovorima kod Ride objekta je istog formata kao i u request-u
- Cancel ride od strane putnika (/api/ride/{id}) promenjen u -> /api/ride/{id}/withdraw - kao odgovor se takodje vraca ride
- Kod kreiranja dokumenata za vozaca izbacen je driverId

1.1.8:

- Ispravak opis-a endpoint-a za brisanje dokumenata vozaca

1.1.9

- /api/passenger/{activationId} -> /api/passenger/activate/{activationId} zbog Srping ambiguous prorblema

1.1.10

- Kod ruta /api/user/{id}/ride, /api/driver/{id}/ride, /api/passenger/{id}/ride u locations listi, uklonjeni atributi address, latitude, longitude, tako da sada ostaju samo deprature i destinations