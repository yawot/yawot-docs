.. _Development coding standard for libCellML:

===============
Coding Standard
===============

This section describes the coding standard for libCellML.

.. contents::

Overview
========

The coding standard for libCellML is a list of directives on how code should look when written so that the entire codebase has a similar look and feel irrespective of who has written it.

Style
=====

* C++ code style should follow the example given below

.. code-block:: c++

   #include <math.h>

   class Complex
   {
   public:
       Complex(double re, double im)
           : _re(re), _im(im)
       {}
       double modulus() const
       {
           return sqrt(_re * _re + _im * _im);
       }
   private:
       double _re;
       double _im;
   };
   
   void bar(int i)
   {
       static int counter = 0;
       counter += i;
   }
   
   namespace Foo
   {
   namespace Bar
   {
   void foo(int a, int b)
   {
       for (int i = 0; i < a; i++)
       {
           if (i < b)
               bar(i);
           else
           {
               bar(i);
               bar(b);
           }
       }
   }
   } // namespace Bar
   } // namespace Foo

* Class member variables should start with an underscore '_'
* Indentation is set to 4 spaces (no tabs)

Header Inclusion
================

* Include order

  * First header included in .cpp files is the declaration .hpp file for the .cpp file
  * System header files come next
  * Other header files from libCellMl last
  
    