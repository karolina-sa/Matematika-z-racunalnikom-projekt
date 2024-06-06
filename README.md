# Model napovedi odjema električne energije

V projektni nalogi pri predmetu Matematika z računalnikom 2023/24 sem analizirala in napovedovala odjem električne 
energije gospodinjskih odjemalcev. Skozi celoten projekt sem 
uporabljala programski jezik [Python](https://www.python.org/) ter glavne koncepte teorije časovnih vrst.

## Cilj projekta

Cilj projekta pri predmetu Matematika z računalnikom 2023/24 je sestaviti model, ki bo kar se da točno napovedal odjem električne energije 
za celotni naslednji dan, torej za naslednjih $24$ ur.

## Podatki

Podjetje [GEN-I](https://gen-i.si/) je v obliki excel razpredelnice pripravilo tabelo podatkov, sestavljeno iz $7$ stolpcev:

- `DateTimeStartUTC`: univerzalni koordinirani čas, 
- `DateTimeStartCET`: srednjeevropski čas,
- `Odjem ACT`: odjem električne energije gospodinjskih odjemalcev (tistih brez sončne elektrarne),
- `Temperatura ACT`: dejanska temperatura, 
- `Temperatura FC`: s strani GEN-I napovedana temperatura,
- `Sevanje ACT`: dejansko sevanje in
- `Sevanje FC`: s strani GEN-I napovedano sevanje.

Podatki so podani za obdobje od 1. novembra 2021 do 29. februarja 2024,
na vsakih $15$ minut. Tako ima tabela ima vsega skupaj $81696$ vrstic.

Zaradi varnosti podatkov razpredelnica ni objavljena v repozitoriju. 

## Glavne ugotovitve

S pomočjo teorije časovnih vrst pridemo do 
modela napovedi odjema električne energije gospodinjskih odjemalcev. 
Kot optimalen model izberemo **SARIMAX(4,1,5)(0,1,0)[96]-GARCH(1,3)**.

Napoved izbranega modela dobro opisuje dejanske vrednosti, kar je lepo razvidno iz grafov napovedi ter vrednosti napak. 
Formalno, povprečna napaka RMSE znaša okrog $260$, 
MAPE pa $1{,}5~\%$. Tekom dela ugotovimo tudi, da vključitev eksogenih podatkov prispeva k bolj točni napovedi. 

## Git repozitorij

- Mapa `kratko_porocilo` vsebuje poročilo `kratko_porocilo.pdf`, ki predstavi motivacijo in osnovno analizo podatkov pred pričetkom resnega dela.
- Mapa `porocilo` vsebuje glavno poročilo (datoteka `porocilo_KS.pdf`).
- V mapi `predstavitev` je predstavitev projektne naloge (datoteka `predstavitev_KS.pdf`)
- `napredna_analiza.ipynb` je datoteka s celotno koda in rezultati analize.
- `napoved_za_poljubni_dan.ipynb` vsebuje funkcijo **napoved_z_SARIMA_GARCH**, ki izriše prileganje grafa napovedi (po modelu SARIMAX(4,1,5)(0,1,0)[96]-GARCH(1,3) z upoštevanjem eksogenih podatkov temperature in sevanja) dejanskemu odjemu. Prav tako izpiše napaki RMSE in MAPE.
- `porocilo_KS.pdf` je zaključna verzija poročila projekta.
