
# Scrape data
## What is that!
* Ethical Web Scraping: ask the website owner for permission to retrieve the data automatically. 


## Example

http://www.summet.com/dmsi/html/codesamples/addresses.html


```python
import requests
import re

url = 'http://www.summet.com/dmsi/html/codesamples/addresses.html'
response = requests.get(url)
htmlStr = response.content.decode('ascii')
type(htmlStr)
```

>
>     str
>


```python
print(htmlStr)
```

>     <html>
>     <head><title>Sample Addresses!</title></head>
>     <body>
>     <h1> A page full of sample addresses for your parsing enjoyment!</h1>
>     <h2> (All data is random....)</h2>
>     <ul>
>     <li>Cecilia Chapman<br/>711-2880 Nulla St.<br/>Mankato Mississippi 96522<br/>(257) 563-7401</li>
>     <li>Iris Watson<br/>P.O. Box 283 8562 Fusce Rd.<br/>Frederick Nebraska 20620<br/>(372) 587-2335</li>
>     <li>Celeste Slater<br/>606-3727 Ullamcorper. Street<br/>Roseville NH 11523<br/>(786) 713-8616</li>
>     <li>Theodore Lowe<br/>Ap #867-859 Sit Rd.<br/>Azusa New York 39531<br/>(793) 151-6230</li>
>     <li>Calista Wise<br/>7292 Dictum Av.<br/>San Antonio MI 47096<br/>(492) 709-6392</li>
>     <li>Kyla Olsen<br/>Ap #651-8679 Sodales Av.<br/>Tamuning PA 10855<br/>(654) 393-5734</li>
>     <li>Forrest Ray<br/>191-103 Integer Rd.<br/>Corona New Mexico 08219<br/>(404) 960-3807</li>
>     <li>Hiroko Potter<br/>P.O. Box 887 2508 Dolor. Av.<br/>Muskegon KY 12482<br/>(314) 244-6306</li>
>     <li>Nyssa Vazquez<br/>511-5762 At Rd.<br/>Chelsea MI 67708<br/>(947) 278-5929</li>
>     <li>Lawrence Moreno<br/>935-9940 Tortor. Street<br/>Santa Rosa MN 98804<br/>(684) 579-1879</li>
>     <li>Ina Moran<br/>P.O. Box 929 4189 Nunc Road<br/>Lebanon KY 69409<br/>(389) 737-2852</li>
>     <li>Aaron Hawkins<br/>5587 Nunc. Avenue<br/>Erie Rhode Island 24975<br/>(660) 663-4518</li>
>     <li>Hedy Greene<br/>Ap #696-3279 Viverra. Avenue<br/>Latrobe DE 38100<br/>(608) 265-2215</li>
>     <li>Melvin Porter<br/>P.O. Box 132 1599 Curabitur Rd.<br/>Bandera South Dakota 45149<br/>(959) 119-8364</li>
>     <li>Keefe Sellers<br/>347-7666 Iaculis St.<br/>Woodruff SC 49854<br/>(468) 353-2641</li>
>     <li>Joan Romero<br/>666-4366 Lacinia Avenue<br/>Idaho Falls Ohio 19253<br/>(248) 675-4007</li>
>     <li>Davis Patrick<br/>P.O. Box 147 2546 Sociosqu Rd.<br/>Bethlehem Utah 02913<br/>(939) 353-1107</li>
>     <li>Leilani Boyer<br/>557-6308 Lacinia Road<br/>San Bernardino ND 09289<br/>(570) 873-7090</li>
>     <li>Colby Bernard<br/>Ap #285-7193 Ullamcorper Avenue<br/>Amesbury HI 93373<br/>(302) 259-2375</li>
>     <li>Bryar Pitts<br/>5543 Aliquet St.<br/>Fort Dodge GA 20783<br/>(717) 450-4729</li>
>     <li>Rahim Henderson<br/>5037 Diam Rd.<br/>Daly City Ohio 90255<br/>(453) 391-4650</li>
>     <li>Noelle Adams<br/>6351 Fringilla Avenue<br/>Gardena Colorado 37547<br/>(559) 104-5475</li>
>     <li>Lillith Daniel<br/>935-1670 Neque. St.<br/>Centennial Delaware 48432<br/>(387) 142-9434</li>
>     <li>Adria Russell<br/>414-7533 Non Rd.<br/>Miami Beach North Dakota 58563<br/>(516) 745-4496</li>
>     <li>Hilda Haynes<br/>778-9383 Suspendisse Av.<br/>Weirton IN 93479<br/>(326) 677-3419</li>
>     <li>Sheila Mcintosh<br/>P.O. Box 360 4407 Et Rd.<br/>Santa Monica FL 30309<br/>(746) 679-2470</li>
>     <li>Rebecca Chambers<br/>P.O. Box 813 5982 Sit Ave<br/>Liberal Vermont 51324<br/>(455) 430-0989</li>
>     <li>Christian Emerson<br/>P.O. Box 886 4118 Arcu St.<br/>Rolling Hills Georgia 92358<br/>(490) 936-4694</li>
>     <li>Nevada Ware<br/>P.O. Box 597 4156 Tincidunt Ave<br/>Green Bay Indiana 19759<br/>(985) 834-8285</li>
>     <li>Margaret Joseph<br/>P.O. Box 508 3919 Gravida St.<br/>Tamuning Washington 55797<br/>(662) 661-1446</li>
>     <li>Edward Nieves<br/>928-3313 Vel Av.<br/>Idaho Falls Rhode Island 37232<br/>(802) 668-8240</li>
>     <li>Imani Talley<br/>P.O. Box 262 4978 Sit St.<br/>Yigo Massachusetts 50654<br/>(477) 768-9247</li>
>     <li>Bertha Riggs<br/>P.O. Box 206 6639 In St.<br/>Easthampton TN 31626<br/>(791) 239-9057</li>
>     <li>Wallace Ross<br/>313 Pellentesque Ave<br/>Villa Park Hawaii 43526<br/>(832) 109-0213</li>
>     <li>Chester Bennett<br/>3476 Aliquet. Ave<br/>Minot AZ 95302<br/>(837) 196-3274</li>
>     <li>Castor Richardson<br/>P.O. Box 902 3472 Ullamcorper Street<br/>Lynchburg DC 29738<br/>(268) 442-2428</li>
>     <li>Sonya Jordan<br/>Ap #443-336 Ullamcorper. Street<br/>Visalia VA 54886<br/>(850) 676-5117</li>
>     <li>Harrison Mcguire<br/>574-8633 Arcu Street<br/>San Fernando ID 77373<br/>(861) 546-5032</li>
>     <li>Malcolm Long<br/>9291 Proin Road<br/>Lake Charles Maine 11292<br/>(176) 805-4108</li>
>     <li>Raymond Levy<br/>Ap #643-7006 Risus St.<br/>Beaumont New Mexico 73585<br/>(715) 912-6931</li>
>     <li>Hedley Ingram<br/>737-2580 At Street<br/>Independence Texas 87535<br/>(993) 554-0563</li>
>     <li>David Mathews<br/>1011 Malesuada Road<br/>Moscow Kentucky 77382<br/>(357) 616-5411</li>
>     <li>Xyla Cash<br/>969-1762 Tincidunt Rd.<br/>Boise CT 35282<br/>(121) 347-0086</li>
>     <li>Madeline Gregory<br/>977-4841 Ut Ave<br/>Walla Walla Michigan 82776<br/>(304) 506-6314</li>
>     <li>Griffith Daniels<br/>6818 Eget St.<br/>Tacoma AL 92508<br/>(425) 288-2332</li>
>     <li>Anne Beasley<br/>987-4223 Urna St.<br/>Savannah Illinois 85794<br/>(145) 987-4962</li>
>     <li>Chaney Bennett<br/>P.O. Box 721 902 Dolor Rd.<br/>Fremont AK 19408<br/>(187) 582-9707</li>
>     <li>Daniel Bernard<br/>P.O. Box 567 1561 Duis Rd.<br/>Pomona TN 08609<br/>(750) 558-3965</li>
>     <li>Willow Hunt<br/>Ap #784-1887 Lobortis Ave<br/>Cudahy Ohio 31522<br/>(492) 467-3131</li>
>     <li>Judith Floyd<br/>361-7936 Feugiat St.<br/>Williston Nevada 58521<br/>(774) 914-2510</li>
>     <li>Seth Farley<br/>6216 Aenean Avenue<br/>Seattle Utah 81202<br/>(888) 106-8550</li>
>     <li>Zephania Sanders<br/>3714 Nascetur St.<br/>Hawthorne Louisiana 10626<br/>(539) 567-3573</li>
>     <li>Calista Merritt<br/>Ap #938-5470 Posuere Ave<br/>Chickasha LA 58520<br/>(693) 337-2849</li>
>     <li>Craig Williams<br/>P.O. Box 372 5634 Montes Rd.<br/>Springdale MO 57692<br/>(545) 604-9386</li>
>     <li>Lee Preston<br/>981 Eget Rd.<br/>Clemson GA 04645<br/>(221) 156-5026</li>
>     <li>Katelyn Cooper<br/>6059 Sollicitudin Road<br/>Burlingame Colorado 26278<br/>(414) 876-0865</li>
>     <li>Lacy Eaton<br/>1379 Nulla. Av.<br/>Asbury Park Montana 69679<br/>(932) 726-8645</li>
>     <li>Driscoll Leach<br/>P.O. Box 120 2410 Odio Avenue<br/>Pass Christian Delaware 03869<br/>(726) 710-9826</li>
>     <li>Merritt Watson<br/>P.O. Box 686 7014 Amet Street<br/>Corona Oklahoma 55246<br/>(622) 594-1662</li>
>     <li>Nehru Holmes<br/>P.O. Box 547 4764 Sed Road<br/>Grand Rapids CT 87323<br/>(948) 600-8503</li>
>     <li>Quamar Rivera<br/>427-5827 Ac St.<br/>Schaumburg Arkansas 84872<br/>(605) 900-7508</li>
>     <li>Hiram Mullins<br/>754-6427 Nunc Ave<br/>Kennewick AL 41329<br/>(716) 977-5775</li>
>     <li>Kim Fletcher<br/>Ap #345-3847 Metus Road<br/>Independence CO 30135<br/>(368) 239-8275</li>
>     <li>Rigel Koch<br/>P.O. Box 558 9561 Lacus. Road<br/>Laughlin Hawaii 99602<br/>(725) 342-0650</li>
>     <li>Jeanette Sharpe<br/>Ap #364-2006 Ipsum Avenue<br/>Wilmington Ohio 91750<br/>(711) 993-5187</li>
>     <li>Dahlia Lee<br/>1293 Tincidunt Street<br/>Atwater Pennsylvania 76865<br/>(882) 399-5084</li>
>     <li>Howard Hayden<br/>P.O. Box 847 8019 Facilisis Street<br/>Joliet SC 73490<br/>(287) 755-9948</li>
>     <li>Hyatt Kramer<br/>1011 Massa Av.<br/>Kent ID 63725<br/>(659) 551-3389</li>
>     <li>Sonya Ray<br/>Ap #315-8441 Eleifend Street<br/>Fairbanks RI 96892<br/>(275) 730-6868</li>
>     <li>Cara Whitehead<br/>4005 Praesent St.<br/>Torrance Wyoming 22767<br/>(725) 757-4047</li>
>     <li>Blythe Carroll<br/>7709 Justo. Ave<br/>Princeton TX 77987<br/>(314) 882-1496</li>
>     <li>Dale Griffin<br/>P.O. Box 854 8580 In Ave<br/>Revere South Dakota 43841<br/>(639) 360-7590</li>
>     <li>McKenzie Hernandez<br/>Ap #367-674 Mi Street<br/>Greensboro VT 40684<br/>(168) 222-1592</li>
>     <li>Haviva Holcomb<br/>P.O. Box 642 3450 In Road<br/>Isle of Palms New York 03828<br/>(896) 303-1164</li>
>     <li>Ezra Duffy<br/>Ap #782-7348 Dis Rd.<br/>Austin KY 50710<br/>(203) 982-6130</li>
>     <li>Eleanor Jennings<br/>9631 Semper Ave<br/>Astoria NJ 66309<br/>(906) 217-1470</li>
>     <li>Remedios Hester<br/>487-5787 Mollis St.<br/>City of Industry Louisiana 67973<br/>(614) 514-1269</li>
>     <li>Jasper Carney<br/>1195 Lobortis Rd.<br/>New Orleans New Hampshire 71983<br/>(763) 409-5446</li>
>     <li>Vielka Nielsen<br/>Ap #517-7326 Elementum Rd.<br/>Fort Smith North Dakota 79637<br/>(836) 292-5324</li>
>     <li>Wilma Pace<br/>Ap #676-6532 Odio Rd.<br/>Darlington CO 06963<br/>(926) 709-3295</li>
>     <li>Palmer Gay<br/>557-2026 Purus St.<br/>Watertown TN 07367<br/>(963) 356-9268</li>
>     <li>Lyle Sutton<br/>Ap #250-9843 Elementum St.<br/>South Gate Missouri 68999<br/>(736) 522-8584</li>
>     <li>Ina Burt<br/>Ap #130-1685 Ut Street<br/>Tyler KS 73510<br/>(410) 483-0352</li>
>     <li>Cleo Best<br/>282-8351 Tincidunt Ave<br/>Sedalia Utah 53700<br/>(252) 204-1434</li>
>     <li>Hu Park<br/>1429 Netus Rd.<br/>Reedsport NY 48247<br/>(874) 886-4174</li>
>     <li>Liberty Walton<br/>343-6527 Purus. Avenue<br/>Logan NV 12657<br/>(581) 379-7573</li>
>     <li>Aaron Trujillo<br/>Ap #146-3132 Cras Rd.<br/>Kingsport NH 56618<br/>(983) 632-8597</li>
>     <li>Elmo Lopez<br/>Ap #481-7473 Cum Rd.<br/>Yorba Linda South Carolina 28423<br/>(295) 983-3476</li>
>     <li>Emerson Espinoza<br/>Ap #247-5577 Tincidunt St.<br/>Corpus Christi WI 97020<br/>(873) 392-8802</li>
>     <li>Daniel Malone<br/>2136 Adipiscing Av.<br/>Lima RI 93490<br/>(360) 669-3923</li>
>     <li>Dante Bennett<br/>481-8762 Nulla Street<br/>Dearborn OR 62401<br/>(840) 987-9449</li>
>     <li>Sade Higgins<br/>Ap #287-3260 Ut St.<br/>Wilmington OR 05182<br/>(422) 517-6053</li>
>     <li>Zorita Anderson<br/>1964 Facilisis Avenue<br/>Bell Gardens Texas 87065<br/>(126) 940-2753</li>
>     <li>Jordan Calderon<br/>430-985 Eleifend St.<br/>Duluth Washington 92611<br/>(427) 930-5255</li>
>     <li>Ivor Delgado<br/>Ap #310-1678 Ut Av.<br/>Santa Barbara MT 88317<br/>(689) 721-5145</li>
>     <li>Pascale Patton<br/>P.O. Box 399 4275 Amet Street<br/>West Allis NC 36734<br/>(676) 334-2174</li>
>     <li>Nasim Strong<br/>Ap #630-3889 Nulla. Street<br/>Watervliet Oklahoma 70863<br/>(437) 994-5270</li>
>     <li>Keaton Underwood<br/>Ap #636-8082 Arcu Avenue<br/>Thiensville Maryland 19587<br/>(564) 908-6970</li>
>     <li>Keegan Blair<br/>Ap #761-2515 Egestas. Rd.<br/>Manitowoc TN 07528<br/>(577) 333-6244</li>
>     <li>Tamara Howe<br/>3415 Lobortis. Avenue<br/>Rocky Mount WA 48580<br/>(655) 840-6139</li>
>      </ul> </body></html>
>



```python
pdata = re.findall("\(\d\d\d\) \d{3}-\d{4}", htmlStr)
pdata
```

>
>     ['(257) 563-7401',
>      '(372) 587-2335',
>      '(786) 713-8616',
>      '(793) 151-6230',
>      '(492) 709-6392',
>      '(654) 393-5734',
>      '(404) 960-3807',
>      '(314) 244-6306',
>      '(947) 278-5929',
>      '(684) 579-1879',
>      '(389) 737-2852',
>      '(660) 663-4518',
>      '(608) 265-2215',
>      '(959) 119-8364',
>      '(468) 353-2641',
>      '(248) 675-4007',
>      '(939) 353-1107',
>      '(570) 873-7090',
>      '(302) 259-2375',
>      '(717) 450-4729',
>      '(453) 391-4650',
>      '(559) 104-5475',
>      '(387) 142-9434',
>      '(516) 745-4496',
>      '(326) 677-3419',
>      '(746) 679-2470',
>      '(455) 430-0989',
>      '(490) 936-4694',
>      '(985) 834-8285',
>      '(662) 661-1446',
>      '(802) 668-8240',
>      '(477) 768-9247',
>      '(791) 239-9057',
>      '(832) 109-0213',
>      '(837) 196-3274',
>      '(268) 442-2428',
>      '(850) 676-5117',
>      '(861) 546-5032',
>      '(176) 805-4108',
>      '(715) 912-6931',
>      '(993) 554-0563',
>      '(357) 616-5411',
>      '(121) 347-0086',
>      '(304) 506-6314',
>      '(425) 288-2332',
>      '(145) 987-4962',
>      '(187) 582-9707',
>      '(750) 558-3965',
>      '(492) 467-3131',
>      '(774) 914-2510',
>      '(888) 106-8550',
>      '(539) 567-3573',
>      '(693) 337-2849',
>      '(545) 604-9386',
>      '(221) 156-5026',
>      '(414) 876-0865',
>      '(932) 726-8645',
>      '(726) 710-9826',
>      '(622) 594-1662',
>      '(948) 600-8503',
>      '(605) 900-7508',
>      '(716) 977-5775',
>      '(368) 239-8275',
>      '(725) 342-0650',
>      '(711) 993-5187',
>      '(882) 399-5084',
>      '(287) 755-9948',
>      '(659) 551-3389',
>      '(275) 730-6868',
>      '(725) 757-4047',
>      '(314) 882-1496',
>      '(639) 360-7590',
>      '(168) 222-1592',
>      '(896) 303-1164',
>      '(203) 982-6130',
>      '(906) 217-1470',
>      '(614) 514-1269',
>      '(763) 409-5446',
>      '(836) 292-5324',
>      '(926) 709-3295',
>      '(963) 356-9268',
>      '(736) 522-8584',
>      '(410) 483-0352',
>      '(252) 204-1434',
>      '(874) 886-4174',
>      '(581) 379-7573',
>      '(983) 632-8597',
>      '(295) 983-3476',
>      '(873) 392-8802',
>      '(360) 669-3923',
>      '(840) 987-9449',
>      '(422) 517-6053',
>      '(126) 940-2753',
>      '(427) 930-5255',
>      '(689) 721-5145',
>      '(676) 334-2174',
>      '(437) 994-5270',
>      '(564) 908-6970',
>      '(577) 333-6244',
>      '(655) 840-6139']
>


```python

```
