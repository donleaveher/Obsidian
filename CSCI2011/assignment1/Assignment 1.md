***Question 1***
	Let $p, q, \text{and}\,r$ be the propositions
		$p$: You get an A on the final exam.
		$q$: You do every exercise in this book.
		$r$: You get an A in the class
	$a)\quad \neg q \land r$
	$b)\quad p\land q\land r$
	$c)\quad r\to p$
	$d)\quad\neg q\land p\land r$
	$e)\quad (p\land q)\to r$
	$f)\quad r\leftrightarrow(p\lor q)$

***Question 2***
	Determine whether each of these conditional statement is true or false
	$a)\quad$True
	$b)\quad$True
	$c)\quad$False
	$d)\quad$True
*Tips*: The statement will wrong only if the 'if' statement is correct and 'then' statement is wrong.

***Question 3***
	For each of these sentences, determine whether an inclusive or, or an exclusive or.
	$a)\quad$**Inclusive or** : It always required by some firms when they hire people, people who can use Java or C++ or both are satisfied
	$b)\quad$ **Exclusive or** : When we order the food in the restaurant, we only can choose one of than only.
	$c)\quad$ **Inclusive or** : When entering other country, the officer will require certifications which can represent your ID.
	$d)\quad$ **Exclusive or**: These two words are contradict.

***Question 4***
	State the converse, contrapositive, and inverse of each of these conditional statements. 
		Converse: If i stay at home, then it snows tonight.
		Inverse: If it does not snow tonight, then I will go out.
		Contrapositive: If i go out, then it does not snow tonight.                                                              
		Converse: I go to the beach, then It is sunny summer day.
		Inverse: It is not sunny summer day, I will not go to the beach.
		Contrapositive: I will not go to the beach, then it is not sunny summer day.                                
		Converse: If i sleep until noon, then i stay up late.
		Inverse: If i do not stay up late, then i will not sleep until noon.
		Contrapositive: If i do not sleep until not, then i do not stay up late.

***Question 5***
	Show that $\neg p\to (q\to r)$ and $q\to(p\lor r)$ are logically equivalent.
$$
\begin{align*}
\neg p \to (q \to r) &\equiv p \lor (q \to r) \\
p \lor (q \to r)&\equiv p \lor (\neg q \lor r) \\
p \lor (\neg q \lor r) &\equiv \neg q\lor(p\lor r) \\ 
&\equiv q \to (p \lor r)
\end{align*}
$$

***Question 6***
	For each of these compound propositions, use the conditional-disjunction equivalence to find an equivalent compound proposition that does not involve conditions.
$$\begin{align*}
\neg p \to \neg q&\equiv \neg q\lor p\\
\\
\quad\quad (p\lor q)\to \neg p&\equiv \neg(p\lor q)\lor \neg p\\
&\equiv\neg p \land\neg q\lor\neg p\\
&\equiv \neg p\\
\\
(p\to \neg q)\to(\neg p\to q)&\equiv \neg(p\to \neg q)\lor(\neg p\to q)\\
&\equiv\neg(\neg p\lor\neg q)\lor(p\lor q)\\
&\equiv\neg(\neg(p\land q))\lor(p\lor q)\\
&\equiv(p\land q)\lor(p\lor q)\\
&\equiv p\lor q
\end{align*}$$
