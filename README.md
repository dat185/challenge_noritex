# challenge_noritex

Your task is to implement the function evaluate below to the specification
provided in the documentation string. If the documentation is in any
way ambiguous, please email Nessim Btesh for clarification.
If you feel that auxiliary helper functions would be helpful, feel free to
write them. You may change anything in this file except you are not permitted
to alter the name or function signature of evaluate().

Although we provide you with some test cases, do not assume that these cover
all corner cases, and we may use a different set of inputs to validate your
solution. We will be looking at your solution both for correctness and for
style.

Best of luck!

------

 """Evaluate all of the values in the spreadsheet.

    Given a matrix m of "arbitrary" size, evalute all of the cells in the
    spreadsheet and return the matrix with everything computed. We will assume
    that columns are denoted using a letter while rows are denoted by numbers.
    E.g "A1" is equivalent to ``m[0][0]`` while "C23" is ``m[22][2]``. 

    As such, here are some examples, assume we have the matrix:

        1   2
        3   4

    This, obviously, should just return the same matrix. Now, let's add some
    functions:

        1   =A1
        2   =A2 + 1

    This should evalute to:

        1   1
        2   3

    Now, let's take this one step further and add in a second level of
    reference:

        1           =A1 + 1
        =B1 + 1     =A2 + B1

    This should evalute to:

        1   2
        3   5

    If you are given a reference to a cell that has not been defined, you
    should raise a ReferenceError. For example, this should not work:

        1           =A5 + 2
        =B1 + 1     =A2 + 1

    If you find circular references, you should raise a ValueError. For example:

        =B1 + 1     =A1 + 1

    You can assume the following:
        - All "functions" will have = as the first character
        - The only operations that will be peformed are +, -, *, /
        - All input numbers will be integers (you may have some floats as a 
          result of division, however)
        - Each "function" will only be a direct reference or binary operation.
          I.e. It'll either be something like "=A1" or "=A1 + 1" but not
          "=A1 + 1 + 2"
        - Spaces in "functions" are meaningless. I.e. "=A1 + 1" is the same as
          "=A1+1" or "= A1  +   1". However, a negative sign must appear 
          right in front of the number. E.g. "=A1 +   -1" is valid, but
          "=A1 +  -  1" is not
        - There will be no column that goes past "Z" and capitalization in
          column names is ignored. I.e. "A1" is the same as "a1".

    :param m: The matrix to be evaluated. Each of the entries in the matrix
              will either be numbers or strings.
    :returns: A matrix of the same dimensions as :attr:`m` with all of the
              functions evaluated. All of the entries in this returned matrix
              should be numeric and not strings.
    :raises:
        :ValueError: If there is a problem parsing any of the input values
        :ReferenceError: If a cell is referenced that has not been defined
        :ValueError: If there is a circular reference
        :ZeroDivisionError: If there is a divide by zero
