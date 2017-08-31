# HTMLandNIF
BASH program to map an HTML (parse to plain text) to NIF, validating the results with RDFUnit.

 The program takes as input an HTML and a prefix. The output is an HTML (the input html) with NIF results attached it in the <head> section as a <script> tag, just as mention in https://www.w3.org/TR/turtle/#in-html.

      Example:

      ./bash_validation_v0.1.sh -f Data/final.html -p "http://myprefix.com" -u /home/julio/Downloads/RDFUnit-0.8.1/

       where:

                  -**f** is the file to be processed
                  -**p** is the prefix submitted by the user
                  -**u** is the path of RDFUnit

      The -u parameter was defined because when running RDFUnit outside their main folder it does not work. But if RDFUnit is run it in their main folder it works normally.

       The spotlight evaluation was made as follows:
       
      curl -X POST http://api.dbpedia-spotlight.org/rest/annotate --data "text=$TEXTCONT" --data "prefix=$PREFIX" --data "confidence=0.5" -H "Accept:text/turtle"

       where **$FILE** is the html file, **$PREFIX** is the prefix given by the user and **$TEXTCONT** is the plain text of the Html file

       The NIF validation was made as follows:

                  bin/rdfunit-dev -d $FILEPATHSPOT -s nif -o html

       where **$FILEPATHSPOT** is the output of spotlight.
