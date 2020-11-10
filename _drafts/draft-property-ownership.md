https://datamade.us/blog/parsing-addresses-with-usaddress/

usaddress -> good starting point
  but breaks with things like
    SCHUTZBERG, ARNOLD & FRANCES SCHUTZBERG,
    TRS. THE SCHUTZBERG REALTY TRUST
    19 DAVENPORT ST
    CAMBRIDGE, MA 02140

can't be the first number -- 19 Fayette St Trust


SPINOS, CONSTANCE, TR.
OF FAYETTE 62 REALTY TRUST
C/O ELAINE PITENIS
2828 N. ATLANTIC AVE STE #806
DAYTONA BEACH, FL 32118


Even has trouble with:
ELAINE PITENIS 2828 N. ATLANTIC AVE STE #806 DAYTONA BEACH, FL 32118

But pulling the # out of it helped.




So...

[ ] break after C/O line
[ ] break before number when it's at start of line
[ ] strip #'s as a way to normalize

OR should I add complex recipients by training usaddress?
  -> no, that's more work than it's worth right now

run through the addresses

output failed addresses
  (missing any of: AddressNumber, StreetName, StreetNamePostType, PlaceName, StateName, ZipCode)

report failed addresses,
  tag them
  make variants
  train

THEN:
  Need to figure out property ownership
  and company connection

Make a spreadsheet of common tokens like TRS., LLC, TRUSTEE(S), etc., and create a spacy model with that.
Take 50 or so, replace text (shuffle first and last names around, change street names), turn into training JSON
  https://spacy.io/api/annotation#vocab-jsonl
  https://spacy.io/api/lexeme#attributes
  https://spacy.io/api/annotation#json-input
  https://spacy.io/usage/training#ner
    ex: https://github.com/explosion/spaCy/blob/master/examples/training/training-data.json
Pop into spacy




pipenv
(pipenv shell)
pipenv run python3
