



 

 

 

 

 

([C++](Cpp.htm)) [RemoveExtension](CppRemoveExtension.htm)
==========================================================

 

[std::string](CppString.htm) [code snippet](CppCodeSnippets.htm) to
remove a filename's extension.

 

  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` //From http://www.richelbilderbeek.nl/CppRemoveExtension.htm const std::string RemoveExtension(const std::string& filename) {   const int dot_index = filename.rfind(".",filename.size());   assert(dot_index != -1 && "No dot found in filename");   return filename.substr(0,dot_index); }`
  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 





 

[![Valid XHTML 1.0 Strict](valid-xhtml10.png){width="88"
height="31"}](http://validator.w3.org/check?uri=referer)