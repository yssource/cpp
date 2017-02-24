



 

 

 

 

 

([C++](Cpp.htm)) [StripXmlTag](CppStripXmlTag.htm)
==================================================

 

[StripXmlTag](CppStripXmlTag.htm) is an [XML](CppXml.htm) [code
snippet](CppCodeSnippets.htm) to remove the outer tags of an
[XML](CppXml.htm) element.

 

-   [Download the Qt Creator project
    'CppStripXmlTag' (zip)](CppStripXmlTag.zip)

 

 

 

 

 

Technical facts
---------------

 

[Application type(s)](CppApplication.htm)

-   ![Desktop](PicDesktop.png) [Desktop
    application](CppDesktopApplication.htm)

[Operating system(s) or programming environment(s)](CppOs.htm)

-   ![Lubuntu](PicLubuntu.png) [Lubuntu](CppLubuntu.htm) 12.04 (precise)

[IDE(s)](CppIde.htm):

-   ![Qt Creator](PicQtCreator.png) [Qt Creator](CppQtCreator.htm) 2.4.1

[Project type](CppQtProjectType.htm):

-   ![console](PicConsole.png) [Console
    application](CppConsoleApplication.htm)

[C++ standard](CppStandard.htm):

-   ![C++98](PicCpp98.png) [C++98](Cpp98.htm)

[Compiler(s)](CppCompiler.htm):

-   [G++](CppGpp.htm) 4.6.3

[Libraries](CppLibrary.htm) used:

-   ![STL](PicStl.png) [STL](CppStl.htm): GNU ISO C++ Library, version
    4.6.3

 

 

 

 

 

[Qt project file](CppQtProjectFile.htm): CppStripXmlTag.pro
-----------------------------------------------------------

 

  -------------------------------------------------------------------------------------------------------------------------------------------
  ` QT       -= core QT       -= gui TARGET = CppStripXmlTag CONFIG   += console CONFIG   -= app_bundle TEMPLATE = app SOURCES += main.cpp`
  -------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

main.cpp
--------

 

  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include <cassert> #include <string>  ///Strip the XML tags of an XML item ///For example '<tag>text</tag>' becomes 'text' ///Note that also '<any_tag>text</other_tag>' fails ///From http://www.richelbilderbeek.nl/CppStripXmlTag.htm const std::string StripXmlTag(const std::string& s) {   if (s.empty()) return "";   if (s[0]!='<') return "";   if (s[s.size() - 1]!='>') return "";   const std::size_t begin = s.find_first_of('>');   if (begin == std::string::npos) return "";   const std::size_t end = s.find_last_of('<');   if (end == std::string::npos) return "";   if (begin > end) return "";   assert(begin < end);   const std::string tag_left = s.substr(0,begin+1);   assert(!tag_left.empty());   assert(tag_left[0] == '<');   assert(tag_left[tag_left.size() - 1] == '>');   const std::string tag_left_text = tag_left.substr(1,tag_left.size() - 2);   if (tag_left_text.empty()) return "";   const std::string tag_right = s.substr(end,s.size() - end);   if (tag_right.size() < 2) return "";   assert(!tag_right.empty());   assert(tag_right[0] == '<');   assert(tag_right[tag_right.size() - 1] == '>');   const std::string tag_right_text = tag_right.substr(2,tag_right.size() - 3);   if (tag_right_text.empty()) return "";   if (tag_left_text != tag_right_text) return "";   const std::string text = s.substr(begin + 1,end - begin - 1);   return text; }   int main() {   assert(StripXmlTag("<my_tag>text</my_tag>") == "text");   assert(StripXmlTag("<mytag>text</mytag>") == "text");   assert(StripXmlTag("<tags>text</tags>") == "text");   assert(StripXmlTag("<tag>text</tag>") == "text");   assert(StripXmlTag("<tg>text</tg>") == "text");   assert(StripXmlTag("<t>text</t>") == "text");   assert(StripXmlTag("<x>y</x>") == "y");   assert(StripXmlTag("<x>y</x></x>") == "y</x>");   assert(StripXmlTag("<x><x>y</x>") == "<x>y");   assert(StripXmlTag("<x><x>y</x></x>") == "<x>y</x>");   assert(StripXmlTag("<x>y</z>") == "");   assert(StripXmlTag("<x>y<x>") == "");   assert(StripXmlTag("<>y<>") == "");   assert(StripXmlTag("<>y</>") == "");   assert(StripXmlTag("<x>y") == "");   assert(StripXmlTag("<x></x>") == ""); }`
  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 





 

[![Valid XHTML 1.0 Strict](valid-xhtml10.png){width="88"
height="31"}](http://validator.w3.org/check?uri=referer)

This page has been created by the [tool](Tools.htm)
[CodeToHtml](ToolCodeToHtml.htm)