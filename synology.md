# Selbst installierte Programme mit ipkg
Um Programme, die selbst installiert wurden mit ipkg zu verwenden, muss deren Speicherort in der Pfadvariable 
eingetragen sein. Die ipkg-Binaries werden in /opt/bin abgelegt.
Die Pfadvariable wird mit dem Kommando
`"export PATH=/opt/bin:$PATH"`
manipuliert, wobei der Text vor dem ":" zur Variable hinzugefuegt wurde.