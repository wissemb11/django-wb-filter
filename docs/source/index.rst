Welcome to Lumache's documentation!
===================================

**Lumache** (/lu'make/) is a Python library for cooks and food lovers
that creates recipes mixing random ingredients.
It pulls data from the `Open Food Facts database <https://world.openfoodfacts.org/>`_
and offers a *simple* and *intuitive* API.

Check out the :doc:`usage` section for further information, including
how to :ref:`installation` the project.

.. note::

   This project is under active development.

Contents
--------

.. toctree::

   usage
   apiProduct Brief
wissem boughammoura
Dernière mise à jour :
Hier at 10:10
Negation of Condition simple : NOT "a=10" ( a!=0) 
using default Q operator
>>> ~Q('a=10')
<Q: (NOT (AND: a=10))>

using my Q_kwargs
-----using dictionary-----
>>> Q_kwargs({'~a': 10})
<Q: (NOT (AND: ('a', 10)))>
>>> Q_kwargs({'a': 10},{'negation':True})
<Q: (NOT (AND: ('a', 10)))>https://web.postman.co/request/10715584-2253d227-1037-4e86-829a-1e3efddba95a
-----using list-----
>>> Q_kwargs([{'~a': 10}])
<Q: (NOT (AND: ('a', 10)))>
-----using str-----
>>> Q_kwargs('(~a=10)')
<Q: (NOT (AND: ('a', '10')))>
>>> Q_kwargs('(*a=10)')
<Q: (NOT (AND: ('a', '10')))>

*****************************************************************
Or of 2 Conditions :  "a=1 OR b=2" (a=1|b=2) using default Q operator
>>> Q({'a': 1})|Q({'b': 1})
<Q: (OR: {'a': 1}, {'b': 1})>
>>> ~(~Q({'a': 1})&~Q({'b': 1}))
<Q: (NOT (AND: (NOT (AND: {'a': 1})), (NOT (AND: {'b': 1}))))>
using or_ in "operator" module  and Q operator
import operator
>>> operator.or_(*[Q({'a': 1}),Q({'b': 1})])
<Q: (OR: {'a': 1}, {'b': 1})>
>>> operator.or_(Q({'a': 1}),Q({'b': 1}))
<Q: (OR: {'a': 1}, {'b': 1})>
using my Q_kwargs
-----using dictionary with default option {'logic_and':True}-----
>>> Q_kwargs({'a': 10,'b':20})
<Q: (OR: ('a', 10), ('b', 20))>
>>> Q_kwargs({'a': 10,'b':20},{'logic_and':True})
<Q: (OR: ('a', 10), ('b', 20))>
>>> ~Q_kwargs({'~a': 10,'~b':20},{'logic_and':False})
<Q: (NOT (AND: (NOT (AND: ('a', 10))), (NOT (AND: ('b', 20)))))>
-----using list-----
>>> Q_kwargs([{'a': 10,'b':20}])
<Q: (OR: ('a', 10), ('b', 20))>
>>> Q_kwargs([{'a': 10,'b':20}],{'logic_and':True})
<Q: (OR: ('a', 10), ('b', 20))>
>>> Q_kwargs([{'~a': 10,'~b':20}],{'logic_and':True,'negation':True})
<Q: (NOT (AND: (OR: (NOT (AND: ('a', 10))), (NOT (AND: ('b', 20))))))>
-----using str-----
>>> Q_kwargs('(a=10|b=20)')
<Q: (OR: ('a', '10'), ('b', '20'))>
>>> Q_kwargs('(*(~a=10&~b=20))')
<Q: (NOT (AND: (NOT (AND: (NOT (AND: ('a', '10'))), (NOT (AND: ('b', '20')))))))>

*****************************************************************
AND of 2 Conditions :  "a=1 AND b=2" (a=1&b=2) *******
*****************************************************************

using default Q operator

>>> Q({'a': 1})&Q({'b': 1})
<Q: (AND: {'a': 1}, {'b': 1})>
>>> Q({'a': 1},{'b': 1})
<Q: (AND: {'a': 1}, {'b': 1})>
>>> Q(*[{'a': 1},{'b': 1}])
<Q: (AND: {'a': 1}, {'b': 1})>
>>> ~(~Q({'a': 1})|~Q({'b': 1}))
<Q: (NOT (AND: (OR: (NOT (AND: {'a': 1})), (NOT (AND: {'b': 1})))))>

using or_ in "operator" module  and Q operator

>>> import operator
>>> operator.and_(Q({'a': 1}),Q({'b': 1}))
<Q: (AND: {'a': 1}, {'b': 1})>
>>> operator.and_(*[Q({'a': 1}),Q({'b': 1})])
<Q: (AND: {'a': 1}, {'b': 1})>

using my Q_kwargs
-----using dictionary with option {'logic_and':False}-----
>>> Q_kwargs({'a': 10,'b':20},{'logic_and':False})
<Q: (AND: ('a', 10), ('b', 20))>
>>> ~Q_kwargs({'~a': 10,'~b':20})
<Q: (NOT (AND: (OR: (NOT (AND: ('a', 10))), (NOT (AND: ('b', 20))))))>
>>> ~Q_kwargs({'~a': 10,'~b':20},{'logic_and':True})
<Q: (NOT (AND: (OR: (NOT (AND: ('a', 10))), (NOT (AND: ('b', 20))))))>
-----using list-----
>>> Q_kwargs([{'a': 10,'b':20}],{'logic_and':False})
<Q: (AND: ('a', 10), ('b', 20))>
>>> Q_kwargs([{'~a': 10,'~b':20}],{'logic_and':True,'negation':True})
<Q: (NOT (AND: (OR: (NOT (AND: ('a', 10))), (NOT (AND: ('b', 20))))))>
-----using str-----
>>> Q_kwargs('(a=10&b=20)')
<Q: (AND: (AND: ('a', '10')), (AND: ('b', '20')))>
>>> Q_kwargs('((a=10)&(b=20))')
<Q: (AND: ('a', '10'), ('b', '20'))>
>>> Q_kwargs('(*(~a=10|~b=20))')
<Q: (NOT (AND: (NOT (AND: (OR: (NOT (AND: ('a', '10'))), (NOT (AND: ('b', '20'))))))))>




 OR of more than 2 Conditions :  "a=1 or b=2" (a=1|b=2) 
Same thing as 2 EXCEPT "operator.and_" needs only 2 arguments
using default Q operator
>>> Q(a=1)|Q(a=2)|Q(c=3)|Q(d=4)
<Q: (OR: ('a', 1), ('a', 2), ('c', 3), ('d', 4))>
using my Q_kwargs
-----using dictionary-One Expression of reunion de la form (A | B | C |....| D) with default option {'logic_and':True}-------
>>> Q_kwargs({'a': 10,'b':20,'c':30}) #{'logic_and':True}
<Q: (OR: {'a': 10}, {'b': 20}, {'c': 30})>
-----using list-----
>>> Q_kwargs([{'a': 10,'b':20,'c':30}]) #{'logic_and':True}
<Q: (OR: {'a': 10}, {'b': 20}, {'c': 30})>
-----using str THE PARENTHESIS ARE NECESSARY-----
>>> Q_kwargs('(a=1|a=2|c=3|d=4)')
<Q: (OR: ('a', '1'), ('a', '2'), ('c', '3'), ('d', '4'))>
>>> Q_kwargs('((a=1)|(a=2)|(c=3)|(d=4))')
<Q: (OR: ('a', '1'), ('a', '2'), ('c', '3'), ('d', '4https://web.postman.co/request/10715584-2253d227-1037-4e86-829a-1e3efddba95a'))>

AND of 2 Conditions :  "a=1 AND b=2" (a=1&b=2) 

Same thing as 2 EXCEPT "operator.or_" needs only 2 arguments
using default Q operator
>>> Q(a=1)&Q(a=2)&Q(c=3)&Q(d=4)
<Q: (AND: ('a', 1), ('a', 2), ('c', 3), ('d', 4))>
using my Q_kwargs
-----using dictionary-----
-------One Expression of Intersections de la form (A & B & C &....& D) -------
>>> Q_kwargs({'a': 10,'b':20,'c':30},{'logic_and':False})
<Q: (AND: {'a': 10}, {'b': 20}, {'c': 30})>
----using list----
>>> Q_kwargs([{'a': 10,'b':20,'c':30}],{'logic_and':False})
<Q: (AND: {'a': 10}, {'b': 20}, {'c': 30})>
-----using str THE PARENTHESIS ARE NECESSARY-----
>>> Q_kwargs('(a=1&a=2&c=3&d=4)')
<Q: (AND: (AND: ('a', '1')), (AND: ('a', '2')), (AND: ('c', '3')), (AND: ('d', '4')))>
>>> Q_kwargs('((a=1)&(a=2)&(c=3)&(d=4))')
<Q: (AND: ('a', '1'), ('a', '2'), ('c', '3'), ('d', '4'))>
>>> Q_kwargs('((a=1&a=2)&(c=3)&(d=4))')
<Q: (AND: (AND: ('a', '1')), (AND: ('a', '2')), ('c', '3'), ('d', '4'))>
>>> Q_kwargs('((a=1|a=2)|(c=3)|(d=4))')
<Q: (OR: ('a', '1'), ('a', '2'), ('c', '3'), ('d', '4'))>

MORE examples NESTED Conditions
using default Q operator
>>> Q(a=1)&Q(a=2)&Q(c=3)|Q(d=4)
<Q: (OR: (AND: ('a', 1), ('a', 2), ('c', 3)), ('d', 4))>
>>> Q(a=1)|Q(a=2)&Q(c=3)|Q(d=4)
<Q: (OR: ('a', 1), (AND: ('a', 2), ('c', 3)), ('d', 4))>

using my Q_kwargs
-----using dictionary-----

----Negation of all the expression default is {'negation':False}----
>>> Q_kwargs({'~a': 10,'b':20},{'negation':True})
<Q: (NOT (AND: (OR: (NOT (AND: {'a': 10})), {'b': 20})))>
>>> Q_kwargs([{'~a': 10,'b':20}],{'logic_and':False,'negation':True})
<Q: (NOT (AND: (NOT (AND: {'a': 10})), {'b': 20}))>

>>> Q_kwargs({'~a': 10,'b':20},{'negation':False})
<Q: (OR: (NOT (AND: {'a': 10})), {'b': 20})>

>>> Q_kwargs([{'~a': 10,'b':20}],{'logic_and':False,'negation':False})
<Q: (AND: (NOT (AND: {'a': 10})), {'b': 20})>
#Plus d'exemples Q_kwargs:
-----using list-----
-------Multiple INTERSECTION of REUNIONS de la form (A | B | C) & (AA | BB | CC) & (AAA | BBB | CCC) with default option {'logic_and':True}-------
>>> Q_kwargs([{'a': 10,'b':20,'c':30},{'aa': 10,'bb':20,'cc':30},{'aaa': 10,'bbb':20,'ccc':30}]) #ou bien  with default {'logic_and':True
<Q: (AND: (OR: {'a': 10}, {'b': 20}, {'c': 30}), (OR: {'aa': 10}, {'bb': 20}, {'cc': 30}), (OR: {'aaa': 10}, {'bbb': 20}, {'ccc': 30}))>

>>> Q_kwargs([{'a': 10,'b':20,'c':30},{'aa': 10,'bb':20,'cc':30},{'aaa': 10,'bbb':20,'ccc':30}],{'logic_and':True})
<Q: (AND: (OR: {'a': 10}, {'b': 20}, {'c': 30}), (OR: {'aa': 10}, {'bb': 20}, {'cc': 30}), (OR: {'aaa': 10}, {'bbb': 20}, {'ccc': 30}))>

-------Multiple INTERSECTION of REUNIONS de la form (A & B & C) | (AA & BB & CC) | (AAA & BBB & CCC) with  option {'logic_and':False}-------
>>> Q_kwargs([{'a': 10,'b':20,'c':30},{'aa': 10,'bb':20,'cc':30},{'aaa': 10,'bbb':20,'ccc':30}],{'logic_and':False})
<Q: (OR: (AND: {'a': 10}, {'b': 20}, {'c': 30}), (AND: {'aa': 10}, {'bb': 20}, {'cc': 30}), (AND: {'aaa': 10}, {'bbb': 20}, {'ccc': 30}))>




-----using str-----
>>> Q_kwargs('(*id=1)')
<Q: (NOT (AND: ('id', '1')))>
>>> Q_kwargs('(-id=1)')
<Q: (AND: ('-id', '1'))>
>>> Q_kwargs('(*(*-id=1))')
<Q: (NOT (AND: (NOT (AND: (NOT (AND: ('-id', '1')))))))>
>>> Q_kwargs('(*(*-id=1)|(https://web.postman.co/request/10715584-2253d227-1037-4e86-829a-1e3efddba95aj=10))')
<Q: (OR: (NOT (AND: ('-id', '1'))), ('j', '10'))>
>>> Q_kwargs('(*-id=1&-id=1)')
<Q: (NOT (AND: (AND: ('-id', '1')), (AND: ('-id', '1'))))>
>>> Q_kwargs('(*(id=1&id=1))')
<Q: (NOT (AND: (NOT (AND: (AND: ('id', '1')), (AND: ('id', '1'))))))>
>>> Q_kwargs('(*(id=1|id=1))')
<Q: (NOT (AND: (NOT (AND: (OR: ('id', '1'), ('id', '1'))))))>
>>> Q_kwargs('(*(-id=1|id=1))')
<Q: (NOT (AND: (NOT (AND: (OR: ('-id', '1'), ('id', '1'))))))>
>>> Q_kwargs('(*-id=1)')
<Q: (NOT (AND: ('-id', '1')))>
>>> Q_kwargs('(*(*-id=1|id=1))')
<Q: (NOT (AND: (NOT (AND: (NOT (AND: (OR: ('-id', '1'), ('id', '1'))))))))>
>>> Q_kwargs('(*(*-id=1|id=1)&(*k=55555&l=66666666))')
<Q: (AND: (NOT (AND: (OR: ('-id', '1'), ('id', '1')))), (NOT (AND: (AND: ('k', '55555')), (AND: ('l', '66666666')))))>
>>> Q_kwargs('(((*-id=1|id=1)&(*k=55555&l=66666666))*)')
<Q: (NOT (AND: ))>
>>> Q_kwargs('((*-id=1)&(-id=1))')
<Q: (AND: (NOT (AND: ('-id', '1'))), ('-id', '1'))>
>>> Q_kwargs('(((*-id=1111&id=22222)|(id=333333&id=444444))&(*k=55555&l=66666666)&(-x=777777|x=888888))')
<Q: (AND: (NOT (AND: (AND: ('k', '55555')), (AND: ('l', '66666666')))), (OR: ('-x', '777777'), ('x', '888888')))>
>>> Q_kwargs('((id=1111&id=22222&id=333333&id=444444&k=55555&l=66666666)|(x=777777|yy=ii))')
<Q: (OR: (AND: (AND: ('id', '1111')), (AND: ('id', '22222')), (AND: ('id', '333333')), (AND: ('id', '444444')), (AND: ('k', '55555')), (AND: ('l', '66666666'))), ('x', '777777'), ('yy', 'ii'))>
>>> Q_kwargs('((id=1111|id=22222|id=333333|id=444444|k=55555|l=66666666)&(x=777777&yy=ii))')
<Q: (AND: (OR: ('id', '1111'), ('id', '22222'), ('id', '333333'), ('id', '444444'), ('k', '55555'), ('l', '66666666')), (AND: ('x', '777777')), (AND: ('yy', 'ii')))>
>>> Q_kwargs('((*-id=1&id=1)|(id=1|-id=1))')



