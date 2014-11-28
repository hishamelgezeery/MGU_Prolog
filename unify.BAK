% Author:
% Date: 11/28/2014

% main function
unify(A,B) :- unify1(A,B).

%helper function unify1 matches each of the cases

%case where the two terms are exactly equal, true is returned.
unify1(X,Y):- X==Y.

%two variables unify:
unify1(X,Y) :- var(X), var(Y), X=Y. % The substitution

% this matches the case when a variable is unified a non-variable.
% a check is done to ensure that the variable X is not part of the term Y, thus avoiding infinite loops
% and therefore generating the most general unifier.
unify1(X,Y) :- var(X), nonvar(Y), \+ contains(X,Y), X=Y. % The substitution
unify1(X,Y) :- var(Y), nonvar(X), unify1(Y,X).

%case where two terms are unified, they are split and each corresponding elements in the lists are unified.
unify1(X,Y) :- nonvar(X), nonvar(Y), functor(X,F,N), functor(Y,F,N),
X =..[F|R], Y =..[F|T], unifyListElements(R,T).

% predicate unifying the corresponding elements of two lists
unifyListElements([],[]).
unifyListElements([X|R],[H|T]) :- unify(X,H), unifyListElements(R,T).

% checks if A exists already in B, either it is equal B or is one of B's members or exists in B's members
contains(A,B) :- A == B.
contains(A,B) :- nonvar(B), functor(B,_,N), contains(A,B,N).
contains(A,[H|T], N):- N1 is N-1, contains(A,H), contains(A,T,N1), !.