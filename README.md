# ConfigEditor##################################################
## Testprojekt "ConfigEditor" f�r Probearbeiten ##
##################################################

##################
## Beschreibung ##
##################

Der "Config-Editor" soll ein Tool sein, mit dem Anwender ohne XML-Kenntnisse eine Config-XML-Datei anlegen und bearbeiten k�nnen.
�ber eine UI kann man dann �nderungen vornehmen, ohne Gefahr zu laufen, die XML zu "besch�digen".

##############################
## Arbeits- und Hilfsmittel ##
##############################

- IDE nach Belieben
- Jegliche Art der Recherche (StackOverflow, etc.)
- Jederzeit Fragen stellen

#################
## Anforderung ##
#################

- Der Code wird in einem git Repository versioniert (Plattform frei w�hlbar, muss zug�nglich sein)
- Der "ConfigEditor" wird als C# Applikation implementiert (Runtime frei w�hlbar)
- Es kann eine neue Config angelegt werden
- Es kann eine bestehende Config ge�ffnet werden
- Die Config wird grafisch in der UI dargestellt
- Es k�nnen Server hinzugef�gt werden
- Es k�nnen Server bearbeitet werden
- Es k�nnen Server entfernt werden
- Es k�nnen Clients hinzugef�gt werden
- Es k�nnen Clients bearbeitet werden
- Es k�nnen Clients entfernt werden
- ConnectionStrings k�nnen als Vorlage separat gespeichert werden
- Die Logik wird �ber Unit Tests abgesichert

##################
## XML-Struktur ##
##################

- Die Config-XML besitzt ein "Config" Root-Node
- "Config" beinhaltet ein "Servers" Node
- "Servers" beinhaltet 0-n "Server" Nodes
- "Server" beinhaltet ein "path" Attribut
- "Server" beinhalten ein "ConnectionString" Node
- "ConnectionString" beinhaltet einen String Value
- "Config" beinhaltet ein "Clients" Node
- "Clients" beinhaltet 0-n "Client" Nodes
- "Client" beinhaltet ein "path" Attribut
- "Client" beinhalten ein "TSClient" Node
- "TSClient" beinhaltet einen Boolean Value

##################
## Leere Config ##
##################

<?xml version="1.0" encoding="utf-8"?>
<Config>
  <Servers>
  </Servers>
  <Clients>
  </Clients>
</Config>

#####################
## Beispiel-Config ##
#####################

<?xml version="1.0" encoding="utf-8"?>
<Config>
  <Servers>
	<Server path="c:\program files (x86)\werbas\werbasweb\server">
	  <ConnectionString>Initial Catalog=WWFirmen;Data Source=.\WERBASWEB;</ConnectionString>
	</Server>
	<Server path="c:\program files (x86)\werbas\werbasweb\serverNightly">
	  <ConnectionString>Initial Catalog=WWFirmen_Nightly;Data Source=.\WERBASWEB;</ConnectionString>
	</Server>
  </Servers>
  <Clients>
	<Client path="c:\program files (x86)\werbas\werbasweb\client">
	  <TSClient>false</TSClient>
	</Client>
	<Client path="c:\program files (x86)\werbas\werbasweb\clientNightly">
	  <TSClient>false</TSClient>
	</Client>
  </Clients>
</Config>

#########
## XSD ##
#########

<xs:schema attributeFormDefault="unqualified" elementFormDefault="qualified" xmlns:xs="http://www.w3.org/2001/XMLSchema">
  <xs:element name="Config">
    <xs:complexType>
      <xs:sequence>
        <xs:element name="Servers">
          <xs:complexType>
            <xs:sequence>
              <xs:element name="Server" maxOccurs="unbounded" minOccurs="0">
                <xs:complexType>
                  <xs:sequence>
                    <xs:element type="xs:string" name="ConnectionString"/>
                  </xs:sequence>
                  <xs:attribute type="xs:string" name="path" use="required"/>
                </xs:complexType>
              </xs:element>
            </xs:sequence>
          </xs:complexType>
        </xs:element>
        <xs:element name="Clients">
          <xs:complexType>
            <xs:sequence>
              <xs:element name="Client" maxOccurs="unbounded" minOccurs="0">
                <xs:complexType>
                  <xs:sequence>
                    <xs:element type="xs:string" name="TSClient"/>
                  </xs:sequence>
                  <xs:attribute type="xs:string" name="path" use="required"/>
                </xs:complexType>
              </xs:element>
            </xs:sequence>
          </xs:complexType>
        </xs:element>
      </xs:sequence>
    </xs:complexType>
  </xs:element>
</xs:schema>