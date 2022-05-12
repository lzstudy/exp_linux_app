Test
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

测试模板
----------------------------------------


Definition lists:

what
  Definition lists associate a term with
  a definition.

how
  The term is a one-line phrase, and the
  definition is one or more paragraphs or
  body elements, indented relative to the
  term. Blank lines are not allowed
  between term and definition.



This is a typical paragraph.  An indented literal block follows.

::

    for(uint8_t i = 0 ; i < 5 ; i++)
        printf("hello world\n");
    echo 1 > hello.txt
    for a in [5,4,3,2,1]:   # this is program code, shown as-is
        print a
    print "it's..."
    # a literal block continues until the indentation ends

This text has returned to the indentation of the first paragraph,
is outside of the literal block, and is therefore treated as an
ordinary paragraph.