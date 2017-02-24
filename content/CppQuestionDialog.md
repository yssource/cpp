



 

 

 

 

 

([C++](Cpp.htm)) [QuestionDialog](CppQuestionDialog.htm)
========================================================

 

[QuestionDialog](CppQuestionDialog.htm) is a dialog for
[Question](CppQuestion.htm).

Technical facts
---------------

 

 

 

 

 

 

./CppQuestionDialog/CppQuestionDialog.pri
-----------------------------------------

 

  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` INCLUDEPATH += \     ../../Classes/CppQtQuestionDialog  SOURCES += \     ../../Classes/CppQtQuestionDialog/questiondialog.cpp  HEADERS  += \     ../../Classes/CppQtQuestionDialog/questiondialog.h  OTHER_FILES += \     ../../Classes/CppQtQuestionDialog/Licence.txt`
  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

./CppQuestionDialog/questiondialog.h
------------------------------------

 

  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` //--------------------------------------------------------------------------- /* QuestionDialog, dialog for Question Copyright (C) 2011-2015 Richel Bilderbeek  This program is free software: you can redistribute it and/or modify it under the terms of the GNU General Public License as published by the Free Software Foundation, either version 3 of the License, or (at your option) any later version.  This program is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.See the GNU General Public License for more details. You should have received a copy of the GNU General Public License along with this program.If not, see <http://www.gnu.org/licenses/>. */ //--------------------------------------------------------------------------- //From http://www.richelbilderbeek.nl/CppQtQuestionDialog.htm //--------------------------------------------------------------------------- #ifndef QUESTIONDIALOG_H #define QUESTIONDIALOG_H  #include <vector>  #pragma GCC diagnostic push #pragma GCC diagnostic ignored "-Weffc++" #pragma GCC diagnostic ignored "-Wunused-but-set-parameter" #pragma GCC diagnostic ignored "-Wunused-local-typedefs" #include <boost/checked_delete.hpp> #include <boost/shared_ptr.hpp> #include <boost/signals2.hpp>  #include "tribool.h" #pragma GCC diagnostic pop  namespace ribi {  struct Question;  ///Dialog for (a derived class of) Question ///For an OpenQuestion use an OpenQuestionDialog ///For a MultipleChoiceQuestion use a MultipleChoiceQuestionDialog struct QuestionDialog {   explicit QuestionDialog();    ///Run the dialog from the command line   void Execute();    Tribool GetIsCorrect() const noexcept { return m_is_correct; }    ///Obtain the question   virtual boost::shared_ptr<const Question> GetQuestion() const = 0;    ///Obtain the version   static std::string GetVersion() noexcept;    ///Obtain the version history   static std::vector<std::string> GetVersionHistory() noexcept;    ///Check if an answer has been submitted   bool HasSubmitted() const { return m_is_correct != Tribool::Indeterminate; }    ///See if the submitted answer is correct   bool IsAnswerCorrect() const;    ///Try to submit an answer   ///For an open question, s will be the anwer   ///For a multiple choice question, s will be the index of the answer   ///Submit will throw an exception if s is invalid. For example,   ///if s is a word, where a multiple choice question needs an index (like '2')   virtual void Submit(const std::string& s) = 0;    virtual std::string ToStr() const noexcept = 0;    ///This signal is emitted when the client requests to quit   mutable boost::signals2::signal<void ()> m_signal_request_quit;    ///This signal is emitted when the client submits an answer, where   ///the boolean indicates if a correct answer was given   mutable boost::signals2::signal<void (bool)> m_signal_submitted;    protected:   virtual ~QuestionDialog() = default;   friend void boost::checked_delete<>(QuestionDialog*);   friend void boost::checked_delete<>(const QuestionDialog*);    ///Set whether the user has answered the client correct   ///and emit m_signal_submitted   void SetIsCorrect(const bool is_correct);    private:    ///Was the submitted answer correct?   ///Emulates a bool*:   ///m_is_correct.empty() -> nullptr -> indeterminate   ///m_is_correct[0] == 0 -> false   ///m_is_correct[0] == 1 -> true   ///Other values and sizes are invalid   //std::vector<int> m_is_correct;   Tribool m_is_correct;    ///The question   //boost::shared_ptr<const Question> m_question;    std::string AskUserForInput() const noexcept;    #ifndef NDEBUG   static void Test() noexcept;   #endif  };  } //~namespace ribi  #endif // OPENQUESTIONDIALOG_H`
  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

./CppQuestionDialog/questiondialog.cpp
--------------------------------------

 

  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` //--------------------------------------------------------------------------- /* QuestionDialog, dialog for Question Copyright (C) 2011-2015 Richel Bilderbeek  This program is free software: you can redistribute it and/or modify it under the terms of the GNU General Public License as published by the Free Software Foundation, either version 3 of the License, or (at your option) any later version.  This program is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.See the GNU General Public License for more details. You should have received a copy of the GNU General Public License along with this program.If not, see <http://www.gnu.org/licenses/>. */ //--------------------------------------------------------------------------- //From http://www.richelbilderbeek.nl/CppQtQuestionDialog.htm //--------------------------------------------------------------------------- #pragma GCC diagnostic push #pragma GCC diagnostic ignored "-Weffc++" #pragma GCC diagnostic ignored "-Wunused-but-set-parameter" #include "questiondialog.h"  #include <cassert> #include <iostream> #include <stdexcept>  #include "openquestion.h" #include "multiplechoicequestion.h" #include "question.h" #include "testtimer.h" #include "trace.h" #pragma GCC diagnostic pop  ribi::QuestionDialog::QuestionDialog()   : m_signal_request_quit{},     m_signal_submitted{},     m_is_correct(Tribool::Indeterminate) {   #ifndef NDEBUG   Test();   #endif   assert(m_is_correct == Tribool::Indeterminate && "Answer is indeterminate at construction");   assert(!HasSubmitted()); }  std::string ribi::QuestionDialog::AskUserForInput() const noexcept {   std::string t;   std::getline(std::cin,t);   return t; }  //std::vector<std::string> ribi::QuestionDialog::GetCorrectAnswers() const noexcept //{ // return this->GetQuestion()->GetAnswers(); //}  void ribi::QuestionDialog::Execute() {   assert(!this->HasSubmitted());    while (!this->HasSubmitted())   {     assert(this->GetQuestion());     std::cout       << (*this->GetQuestion()) << '\n';      std::cout << "Please enter your answer: " << std::endl;      try     {       const std::string s = AskUserForInput();       if (s.empty())       {         m_signal_request_quit();         return;       }        this->Submit(s);       assert(this->HasSubmitted());     }     catch (std::logic_error& e)     {       std::cout         << "Invalid input: " << e.what() << '\n'         << "Please try again or press enter to quit\n"         << '\n';     }   }    std::cout << std::endl;    if (this->IsAnswerCorrect())   {     std::cout << "Correct\n";   }   else   {     const std::vector<std::string> correct_answers { this->GetQuestion()->GetCorrectAnswers() };     std::cout       << "Incorrect, "       << (correct_answers.size() == 1 ? "the correct answer is: " : "the correct answers are: ")       << '\n';     for (const std::string& s: correct_answers)     {       std::cout << "  " << s << '\n';     }   }   std::cout << std::endl; }  std::string ribi::QuestionDialog::GetVersion() noexcept {   return "1.3"; }  std::vector<std::string> ribi::QuestionDialog::GetVersionHistory() noexcept {   return {     "2011-06-29: version 1.0: initial version",     "2013-09-26: version 1.1: improved const-correctness, added noexcept",     "2013-10-24: version 1.2: added Execute for console application",     "2013-10-25: version 1.3: added testing to derived classes"   }; }  bool ribi::QuestionDialog::IsAnswerCorrect() const {   if (!HasSubmitted())   {     throw std::logic_error("Cannot only check if answer is correct, after submitting an answer");   }   assert(HasSubmitted());   return m_is_correct == Tribool::True; }  void ribi::QuestionDialog::SetIsCorrect(const bool is_correct) {   assert(!HasSubmitted() && "Can only answer exactly once");   m_is_correct = is_correct ? Tribool::True : Tribool::False;    assert(HasSubmitted());   assert(IsAnswerCorrect() == is_correct);    m_signal_submitted(is_correct); }   #ifndef NDEBUG void ribi::QuestionDialog::Test() noexcept {   {     static bool is_tested{false};     if (is_tested) return;     is_tested = true;   }   const TestTimer test_timer(__func__,__FILE__,1.0); } #endif`
  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 





 

[![Valid XHTML 1.0 Strict](valid-xhtml10.png){width="88"
height="31"}](http://validator.w3.org/check?uri=referer)

This page has been created by the [tool](Tools.htm)
[CodeToHtml](ToolCodeToHtml.htm)