---
title: The Unified Code for Units of Measure
shortTitle: UCUM
showMiniToc: true
---

# 1 Introduction

The Unified Code for Units of Measure (UCUM) is a code system intended to include all units of measures being contemporarily used in international science, engineering, and business. The purpose is to facilitate unambiguous electronic communication of quantities together with their units. The focus is on electronic communication, as opposed to communication between humans. A typical application of UCUM are electronic data interchange (EDI) protocols, but there is nothing that prevents it from being used in other types of machine communication.

UCUM is inspired by and heavily based on ISO 2955-1983, ANSI X3.50-1986, and HL7's extensions called “ISO+”. The respective ISO and ANSI standards are both entitled “Representation of [...] units in systems with limited character sets” where ISO 2955 refers to SI and other units provided by ISO 1000-1981, while ANSI X3.50 extends ISO 2955 to include U.S. customary units. Because these standards carry the restriction of “limited character sets” in their names they seem to be of less value today, when graphical user interfaces and laser printers are in wide-spread use. For this reason, the european standard ENV 12435 in its clause 7.3 declares ISO 2955 obsolete.

ENV 12435 is dedicated exclusively to the communication of measurements between humans in display and print, and does not provide codes that can be used in communication between systems. It does not even provide a specification that would allow communication of units from one system to the screen or printer of another system. The issue about displaying units in the common style defined by the 9th Conférence Générale des Poids et Mesures (CGPM) in 1947 is not just the character set. Although the Unicode standard and its predecessor ISO/IEC 10646 is the richest character set ever, it is still not enough to specify the presentation of units, because there are important typographical details such as superscripts, subscripts, roman and italics.[^1]

1. ISO 2955 and ANSI X3.50 contain numerous name conflicts, both direct conflicts (e.g., “a” being used for both “year” and “are”) and conflicts that are generated through combination of unit symbols with prefixes (e.g., “ cd” means candela and centi-day and “ PEV” means peta-volt and pico-electronvolt.)

2. Neither ISO 2955 nor ANSI X3.50 cover all units that are currently used in practice. There are many more units in use than what is allowed by the Système International d'Unités (SI) and accompanying standards. For example, the older CGM-units dyne and erg are still used in the science of physiology. Although ANSI X3.50 extends ISO 2955 with some U.S. customary units, it is still not complete in this respect. For example it does not define the degree Fahrenheit.

3. ANSI X3.50 is semantically ambiguous with respect to customary units, even if we do not consider the history and international aspects of customary units. Three systems of mass units are used in the U.S., avoirdupois used generally, apothecaries' used by pharmacists, and troy used in trade with Gold and other precious metals. ANSI X3.50 has no way to select any one of those specifically, which is bad in medicine, where both apothecaries' and avoirdupois weights are being used frequently.

ISO 2955 and all standards that do only look for the resolutions and recommendations of the CGPM and the Comité International des Poids et Mesures (CIPM) as published by the Bureau International des Poids et Mesures (BIPM) and various ISO standards (ISO 1000 and ISO 31) fail to recognize that the needs in practice are often different from the ideal propositions of the CGPM. Although not allowed by the CGPM and related ISO standards, many other units are used in international sciences, healthcare, engineering, and business, both meaningfully and some units of questionable meaning. A coding system that is to be useful in practice must cover the requirements and habits of the practice—even some of the bad habits.

None of the current standards attempt to specify a semantics of units that can be deployed in information systems with moderate requirements. Metrological standards such as those published by the BIPM are dedicated to maximal scientific correctness of reproducible definitions of units. These definitions make sense only to human specialists and can hardly be deployed to their full extent by any information system that is not dedicated to metrology. On the other hand, ISO 2955 and ANSI X3.50 provide no semantics at all for the codes they define.

UCUM provides a single coding system for units that is complete, free of all ambiguities, and that assigns to each defined unit a concise semantics. In communication it is not only important that all communicating parties have the same repertoir of symbols, but also that all attach the same meaning to the symbols they exchange. The common meaning must be computationally verifiable. UCUM assumes a semantics for units based on dimensional analysis.[^2]

In short, each unit is defined relative to a system of base units by a numeric factor and a vector of exponents by which the base units contribute to the unit to be defined. Although we can reflect all the meaning of units covered by dimensional analysis with this vector notation, the following tables do not show these vectors. One reason is that the vectors depend on the base system chosen and even on the ordering of the base units. The other reason is that these vectors are hard to understand to human readers while they can be easily derived computationally. Therefore we define new unit symbols using algebraic terms of other units. Those algebraic terms are also valid codes of UCUM.

# 2 Grammar of Units and Unit Terms

### 2.0.1 Preliminaries

1. The Unified Code for Units of Measure consists of a basic set of terminal symbols for units, called atomic unit symbols or unit atoms, and multiplier prefixes. It also consists of an expression syntax by which these symbols can be combined to yield valid units.

2. The tables of terminal symbols are fixed as of every revision of The Unified Code for Units of Measure, additions, deletions or changes are not allowed.

3. All expression that can be derived from these terminal symbols and the expression syntax are valid codes. Any expression of The Unified Code for Units of Measure has a precisely defined semantics.

The expression syntax of The Unified Code for Units of Measure generates an infinite number of codes with the consequence that it is impossible to compile a table of all valid units.

That the tables of terminal symbols may not be extended does not mean that missing symbols will never be available in The Unified Code for Units of Measure. Suggestions for additions of new symbols are welcome and revisions of The Unified Code for Units of Measure will be released as soon as a change request has been approved.

### 2.0.2 Full and Limited Conformance

1. The semantics of The Unified Code for Units of Measure implies equivalence classes such that different expressions may have the same meaning.

2. Programs that declare full conformance with The Unified Code for Units of Measure must compare unit expressions by their semantics, i.e. they must detect equivalence for different expressions with the same meaning.

3. Programs with limited conformance may compare unit expressions literally and thus may not detect equivalence of unit expressions.

The option for “limited conformace” allows The Unified Code for Units of Measure to be adopted even by less powerful systems that can not or do not want to deal with the full semantics of units. Those systems typically have a table of fixed unit expression literals that may be related to other literals with fixed conversion factors. Although these systems will have difficulties to receive unit expressions from various sources, they will at least send out valid expressions of The Unified Code for Units of Measure, which is an important step towards a commonly used coding scheme for units.

## 2.1 Character Set and Lexical Rules

### 2.1.1 Character Set        

All expressions of The Unified Code for Units of Measure shall be built from characters of the 7-bit US-ASCII character set exclusively.

Terminal unit symbols can consist of all ASCII characters in the range of 33–126 (0x21–0x7E) excluding double quotes (‘"’), parentheses (‘(’ and ‘)’), plus sign (‘+’'), minus sign (‘-’'), period (‘.’'), solidus (‘/’'), equal sign (‘=’'), square brackets (‘[’ and ‘]’), and curly braces (‘{’ and ‘}’), which have special meaning.

A terminal unit symbol can not consist of only digits (‘ 0’–‘9’) because those digit strings are interpreted as positive integer numbers. However, a symbol “10*” is allowed because it ends with a non-digit allowed to be part of a symbol.

For every terminal symbol there is a case insensitive variant defined, to be used when there is a risk of upper and lower case to be confused. Although upper and lower case can be mixed in case insensitive symbols there is no meaning to the case. Case insensitive symbols are incompatible to the case senitive symbols.

The 7-bit US-ASCII character code is the greatest common denominator that can be expected to be available in any communication environment. Only very few units normally require symbols from the greek alphabet and thus the cost of requiring Unicode does not outweigh the benefit. As explained above, the real issue about writing unit terms naturally is not the character set but the ability to write subscripts and superscripts and distinguish roman letters from italics.

Some computer systems or programming languages still have the requirement of case insensitivity and some humans who are not familiar with SI units tend to confuse upper and lower case or can not interpret the difference in upper and lower case correctly. For this reason the case insensitive symbols are defined. Although The Unified Code for Units of Measure does not encourage use of case insensitive symbols where not absolutely necessary, in some circumstances the case insensitive representation may be the greatest common denominator. Thus some systems that can handle case sensitivity may end up using case insensitive symbols in order to communicate with less powerful systems.

ISO 2955 and ANSI X3.50 call case sensitive symbols “mixed case” and case insensitive symbols “single case” and list two columns for “single case” symbols, one for upper case and one for lower case. In The Unified Code for Units of Measure all units can be written in mixed upper and lower case, but in the case insensitive variant the mixing of case does not matter.

White space is not recognized in a a unit term and should generally not occur. UCUM implementations may flag whitespace as an error rather than ignore it. Whitespace is not used as a separator of otherwise ambiguous parts of a unit term.

### 2.1.2 Prefixes

Metric units (cf. §11) may be combinations of a unit symbol with a prefix symbol.

The unit symbol to be combined with the prefix must not itself contain a prefix. Such a prefix-less unit symbol is called unit atom.

Prefix and atom are connected immediately without any delimiter. Separation of an optional prefix from the atom occurs on the lexical level by finding a matching combination of an optional prefix and a unit atom.

The prefix is the longest leading substring that matches a valid prefix where the remainder is a valid metric unit atom. If no such prefix can be matched, the unit atom is without prefix and may be both metric or non-metric. [1–3: ISO 1000, 3; ISO 2955-1983, 3.7; ANSI X3.50-1986, 3.7 (Rule No. 6).]

### 2.1.3 Square Brackets

1. Square brackets (‘[’ and ‘ ]’) may be part of a unit atom at any place but only as matched pairs. Square brackets are lexical elements and not separate syntactical tokens.

2. Within a matching pair of square brackets the full range of characters 33–126 can be used.[^3]

3. Square brackets do not determine the boundary between prefix and unit atom, but they never span the boundary of unit atoms. 

4. Square brackets must not be nested.

For example % “ [abc+ef]”, “ ab[c+ef]”, “ [abc+]ef”, and “ ab[c+ef]” % could all be valid symbols if defined in the tables. In “ab[c+ef]” either “ a” or “ab” could be defined as a prefix, but not “ab[c”.

Square brackets take on one task of round parentheses in HL7's “ISO+” code, where one use of parentheses is to augment unit symbols with suffixes, as in “mm(Hg)”. Another use is to enclose one full unit symbol into parentheses, as “ (ka_u)” (for the King-Armstrong unit of catalytic amount of phosphatase). Apparently, in a unit symbol such enclosed one is supposed not to expect a prefix. Thus, even if “ a_u” would have been defined, “ (ka_u)” should not be matched against kilo- a_u.

Parentheses, however, were also used for the nesting of terms since HL7 version 2.3. At this point it became ambiguous whether parentheses are part of the unit symbol or whether they are syntactic tokens. For instance, “(ka_u)” could mean a nested “ ka_u” (where “k” could possibly be a prefix), but also the proper symbol “ (ka_u)” that happens to have parentheses as part of the symbol. The Unified Code for Units of Measure uses parentheses for the usual meaning of term nesting and uses square brackets where HL7's “ISO+” assumes parentheses to be part of the unit symbol.

§6 curly braces        ■1 The full range of characters 33–126 can be used within a pair of curly braces (‘{’ and ‘ }’). The material enclosed in curly braces is called annotation.    ■2 Annotations do not contribute to the semantics of the unit but are meaningless by definition. Therefore, any fully conformant parser must discard all annotations. Parsers of limited conformace should not value annotations in comparison of units.    ■3 Annotations do, however, signify the end of a unit symbol.    ■4 An annotation without a leading symbol implies the default unit 1 (the unity).    ■5 Curly braces must not be nested.

Curly braces are here because people want annotations and deeply believe that they need annotations. Especially in chemistry and biomedical sciences, there are traditional habits to write annotations at units or instead of units, such as “%vol.”, “RBC”, “CFU”, “kg(wet tis.)”, or “mL(total)”. These habits are hard to overcome. Any attempt of a coding scheme to restrict this percieved expressiveness will ultimately result in the coding scheme not being adopted, or just “half-way” adopted (which is as bad as not adopted).

Two alternative responses to this reality exist: either give in to the bad habits and blow up of the code with dimension- and meaningless unit atoms, or canalize this habit so that it does no harm. The Unified Code for Units of Measure canalizes this habit using curly braces. Nevertheless we do continuing efforts to upgrade doubtful units to genuine units of The Unified Code for Units of Measure by defining and linking them to the other units as good as possible. Thus, “g%” is a valid metric unit atom (so that “mg%” is a valid unit too.) A drops, although quite imprecise, is a valid unit of volume “[drp]”. Even HPF and LPF (the so called “high-” and “low power field” in the microscope) have been defined so that at least they relate to each other.

## 2.2 Syntax Rules

§7 algebraic unit terms        ■1 All units can be combined in an algebraic term using the operators for multiplication (period ‘.‘) and division (solidus ‘/’).   ■2 The multiplication operator is mandatory it must not be omitted or replaced by a space. The multiplication operator is a strict binary operator that may occur only between two unit terms.   ■3 The division operator can be used as a binary and unary operator, i.e. a leading solidus will invert the unit that directly follows it.   ■4 Terms are evaluated from left to right with the period and the solidus having the same operator precedence. Multiple division operators are allowed within one term. [ISO 1000, 4.5.2; ISO 2955-1983, 3.3f; ANSI X3.50-1986, 3.3f (Rule No. 2f).]

The use of the period instead of the asterisk (‘*’) as a multiplication operator continues a tradition codified in ISO 1000 and maintained in ISO 2955. Because floating point numbers may not occur in unit terms the period is not ambiguous. A period in a unit term has no other meaning than to be the multiplication operator.

Since Resolution 7 of the 9th CGPM in 1948 the myth of ambiguity being introduced by more than one solidus lives on and is quoted in all standards concerning the writing of SI units. However, when the strict left to right rule is followed there is no ambiguity, neither with one solidus nor with more than one solidus. However, in human practice we find the tendency to assign a lower precedence to the solidus which misleads people to write a/b·c when they really mean a/(b·c). When this is rewritten as a/b/c there is actually less ambiguity that in a/b·c. So the real source of ambiguity is when a multiplication operator follows a solidus, not when there is more than one solidus in a term. Hence, we remove the restriction for only one solidus and introduce parentheses which may be used to remove any perceived ambiguity.

§8 integer numbers        ■1 A positive integer number may appear in place of a simple unit symbol.   ■2 Only a pure string of decimal digits (‘ 0’–‘9’) is interpreted as a number. If after one or more digits there is any non-digit character found that is valid for unit atoms, all the characters (including the digits) will be interpreted as a simple unit symbol.

For example, the string “123” is a positive integer number while “12a” is a symbol.

Note that the period is only used as a multiplication operator, thus “ 2.5” means 2 × 5 and is not equal to 5/2.

§9 exponents        ■1 Simple units may be raised to a power. The exponent is an integer number and is written immediately behind the unit term. Negative exponents must be preceded by a minus sign (‘ -’ positive exponents may be preceded by an optional plus sign (‘+’).   ■2 If the simple unit raised to a power is a combination of a prefix and a unit atom, both are raised to the power, e.g. “1 cm3” equals “10-6m3” not “10-2m3”. [ISO 2955-1983, 3.5f; ANSI X3.50-1986, 3.5f (Rule No. 4f).]

ISO 2955 and ANSI X3.50 actually do not allow a plus sign leading a positive exponent. However, if there can be any perceived ambiguities, an explicit leading plus sign may be of help sometimes. The Unified Code for Units of Measures therefore allows such plus signs at exponents. The plus sign on positive exponents can be used to delimit exponents from integer numbers used as simple units. Thus, 2+10 means 210 = 1024.

§10 nested terms        ■1 Unit terms with operators may be enclosed in parentheses (‘ (’ and ‘)’) and used in place of simple units. Normal left-to-right evaluation can be overridden with parentheses.   ■2 Parenthesized terms are not considered unit atoms and hence must not be preceded by a prefix.

Up until revision 1.9 there was a third clause “Since a unit term in parenthesis can be used in place of a simple unit, an exponent may follow on a closing parenthesis which raises the whole term within the parentheses to the power.” However this feature was inconsistent with any BNF or other syntax description ever provided, was never used and seems to have no relevant use case. For this reason this clause has been stricken. This is a tentative change. Users who have used this feature in the past, should please comment on this deprecation. If we receive indication that this feature was used by anyone, we would undo the deprecation. If no comments are received, the deprecation continues to take effect.

### Exhibit 1: UCUM syntax in [Backus-Naur form](https://wikipedia.org/wiki/Backus–Naur_form) (BNF)
| Entity              |     | Expression                                                                                                                 |
| ------------------- | --- | -------------------------------------------------------------------------------------------------------------------------- |
| &lt;sign&gt;        | ::= | "+" \| "-"                                                                                                                 |
| &lt;digit&gt;       | ::= | "0" \| "1" \| "2" \| "3" \| "4" \| "5" \| "6" \| "7" \| "8" \| "9"                                                         |
| &lt;digits&gt;      | ::= | &lt;digit&gt;&lt;digits&gt; \| &lt;digit&gt;                                                                               |
| &lt;factor&gt;      | ::= | &lt;digits&gt;                                                                                                             |
| &lt;exponent&gt;    | ::= | &lt;sign&gt;&lt;digits&gt; \| &lt;digits&gt;                                                                               |
| &lt;simple-unit&gt; | ::= | &lt;ATOM-SYMBOL&gt; \| &lt;PREFIX-SYMBOL&gt;&lt;ATOM-SYMBOL\[metric\]&gt;                                                  |
| &lt;annotatable&gt; | ::= | &lt;simple-unit&gt;&lt;exponent&gt; \| &lt;simple-unit&gt;                                                                 |
| &lt;component&gt;   | ::= | &lt;annotatable&gt;&lt;annotation&gt; \| &lt;annotatable&gt; \| &lt;annotation&gt; \| &lt;factor&gt; \| "("&lt;term&gt;")" |
| &lt;term&gt;        | ::= | &lt;term&gt;"."&lt;component&gt; \| &lt;term&gt;"/"&lt;component&gt; \| &lt;component&gt;                                  |
| &lt;main-term&gt;   | ::= | "/"&lt;term&gt; \| &lt;term&gt;                                                                                            |
| &lt;annotation&gt;  | ::= | "{"&lt;ANNOTATION-STRING&gt;"}"                                                                                            |

## 2.3 The Predicate “Metric”

§11 metric and non-metric unit atoms        ■1 Only metric unit atoms may be combined with a prefix.    ■2 To be metric or not to be metric is a predicate assigned to each unit atom where that unit atom is defined.    ■3 All base units are metric. No non-metric unit can be part of the basis.    ■4 A unit must be a quantity on a ratio scale in order to be metric.

The metric predicate accounts for the fact that there are units that are prefixed and others that are not. This helps to disambiguate the parsing of simple units into prefix and atom.

To determine whether a given unit atom is metric or not is not trivial. It is a cultural phenomenon, subject to change, just like language, the meaning of words and how words can be used. At one time we can clearly tell right or wrong useage of words, but these decisions may need to be revised with the passage of time.

Generally, metric units are those defined “in the spirit” of the metric system, that emerged in France of the 18th century and was rapidly adopted by scientists. Metric units are usually based on reproducible natural phenomena and are usually not part of a system of compareable units with different magintudes, especially not if the ratios of these units are not powers of 10. Instead, metric units use multiplier prefixes that magnify or diminish the value of the unit by powers of ten.

Conversely, customary units are in the spirit of the middle age as most of them can be traced back into a time around the 10th century, some are even older from the Roman and Babylonian empires. Most customary units are based on the average size of human anatomical or botanic structures (e.g., foot, ell, fathom, grain, rod) and come in series of comparable units with ratios 1/2, 1/4, 1/12, 1/16, and others. Thus all customary units are non-metric

Not all units from ISO 1000 are metric as degree, minute and second of plane angle are non-metric as well as minute, hour, day, month, and year. The second is a metric unit because it is a part of the SI basis, although it used to be part of a series of customary units (originating in the Babylonian era).

Furthermore, for a unit to be metric it must be a quantity on a ratio scale where multiplication and division with scalars are defined. The Comité Consultatif d'Unités (CCU) decided in February 1995 that SI prefixes may be used with the degree Celsius. This statement has not been made explicitly before. This is an unfortunate decision because difference-scale units like the degree Celsius have no multiplication operation, so that the prefix value could be multiplied with the unit. Instead the prefix at non-ratio units scales the measurement value. One dekameter is 10 times of a meter, but there is no meaning to 10 times of 1 °C in the same way as 30 °C are not 3 times as much as 10 °C. See §§21ff on how The Unified Code for Units of Measure finds a way to accomodate this different use of prefixes at units such as the degree Celsius, bel or neper.

## 2.4 Style

Except for the rule on curly braces (§12), the rules on style govern the creation of the tables of unit atoms not their individual use. Users of The Unified Code for Units of Measure need not care about style rules ( §§13–15) because users just use the symbols defined in the tables. Hence, style rules do not affect conformance to The Unified Code for Units of Measure. New submissions of unit atoms, however, must conform to the style rules.

§12 curly braces        ■1 Curly braces may be used to enclose annotations that are often written in place of units or behind units but that do not have a proper meaning of a unit and do not change the meaning of a unit.    ■2 Annotations have no semantic value.

For example one can write “%{vol}”, “ kg{total}”, or “{RBC}” (for “red blood cells”) as pseudo-units. However, these annotations do not have any effect on the semantics, which is why these example expressions are equivalent to “ %”, “kg”, and “ 1” respectively.

§13 underscore        ■1 When in print a unit would have a subscript, an underscore (‘ _’) is used to separate the subscript from the stem of the unit symbol.   ■2 The subscript is part of the unit atom.    ■3 subscripts are used to disambiguate the two units with the same name but different meanings.

For example when distinguishing the International Table calorie from the thermochemical calorie, we would use 1 calIT or 1 cal th in print. The Unified Code for Units of Measure defines the symbols “ cal_IT” and “ cal_th” with the underscore signifying that “IT” and “th” are subscripts. Other examples are the distinctions between the Julian and Gregorian calendar year from the tropical year or the british imperial gallon from the U.S. gallon (see §31 and §§37ff).

§14 square brackets        ■1 Square brackets enclose suffixes of unit symbols that change the meaning of a unit stem.    ■2 All customary units shall be enclosed completely by square brackets.    ■3 Other unit atoms shall be enclosed in square brackets if they are very rare, if they will conflict with other units, or if they are normally not used as a unit symbol but do have a proper meaning as a unit in The Unified Code for Units of Measure.    ■4 Square brackets are part of the unit atom.

For example 1 m H2O is written as “ m[H2O]” in The Unified Code for Units of Measure because the suffix H 2O changes the meaning of the unit atom for meter (length) to a unit of pressure.

Customary units are defined in The Unified Code for Units of Measure in order to accomodate practical needs. However metric units are still prefered and the customary symbols should not interfere with metric symbols in any way. Thus, customary units are “stigmatized” by enclosing them into square brackets.

If unit symbols for the purpose of display and print are derived from The Unified Code for Units of Measure units, the square brackets can be removed. However, display units are out of scope of The Unified Code for Units of Measure.

§15 apostrophe        ■1 The apostrophe (‘'’) is used to separate words or abbreviated words in a multi-word unit symbol.    ■2 Since units are mathematically defined symbols and not abbreviations of words, multi-word unit symbols should be defined only to reflect existing habits, not in order to create new ones.    ■3 Multi-word units should always be enclosed in square brackets.

For example, such legacy units called “Bodansky unit” or “Todd unit” have the unit symbols “ [bdsk'U]”, and “ [todd'U]” respectively.


# 3 Semantics

§16 preliminaries        ■1 The semantics of The Unified Code for Units of Measure is defined by the algebraic operations of multiplication, division and exponentiation between units, by the equivalence relations of equality and commensurability of units, and by the multiplication of a unit with a scalar.    ■2 Every expression in The Unified Code for Units of Measure is mapped to one and only one semantic element. But every semantic element may have more than one valid representant in The Unified Code for Units of Measure.    ■3 The set of expressions in The Unified Code for Units of Measure is infinite.

§17 equality and commensurability        ■1 The set of expressions in The Unified Code for Units of Measure has two binary, symmetric, reflexive, and transitive relations (equivalence relations) “equals” = and “is commensurable with” ~. All expressions that are equal are also commensurable but not all commensurable expressions are equal.

§18 algebra of units        ■1 The equivalence classes generated by the equality relation = are called units.    ■2 The set of units U has a binary multiplication operator · that is associative and commutative and has the neutral element 1 (so called the unity). For each unit u ∈ U there is an inverse unit u-1 such that u · u-1 = 1. Thus, (U, ·) is an Abelian group.    ■3 The division operation u / v is defined as u · v-1.   ■4 The exponentiation operation with integer exponents n is defined as un = Π1nu.    ■5 The product u' = ru of a real number scalar with the unit u is also a unit, where u' ~ u.

§19 dimension and magnitude        ■1 The equivalence classes generated by the commensurability relation ~ are called dimensions. The set D of dimensions is infinite in principle, but only a finite subset of dimensions are used in practice. Thus, implementations of The Unified Code for Units of Measure need not be able to represent the infinite set of dimensions.    ■2 Two commensurable units that are not equal differ only by their magnitude.    ■3 The quotient u / v of any two commensurable units u ~ v is of the same dimension as the unity (u / v ~ 1). This quotient is also equal to the unity multiplied with a scalar r: u / v = r1, where r is called the relative magnitude of u regarding v.

§20 base units        ■1 Any system of units is constructed from a finite set B of mutually independent base units B = { b1, b2, ..., bn }, on which any other unit u ∈ U is defined as u = r1b1u1 · r2b2u2 · ... · rnbnun, where r = r1 · r2 ·· · rn is called the magnitude of the unit u regarding B.    ■2 With respect to a basis B every unit can thus be represented as a pair (r, û) of magnitude r and dimension û = ( u1, u2, ..., un).    ■3 Two sets of base units are equivalent if there is an isomorphism between the sets of units that they generate.

§19.1 allows to limit the set of supported dimensions. Most practically used units contain exponents of -4 to +4. Thus if memory is limited, 4 bit per component of the dimension vector could be sufficient.

## 3.1 Special Units on non-ratio Scales

§21 special units        ■1 Those symbols that are used as units that imply a measurement on a scale other than a ratio scale (e.g., interval scale, logarithmic scale) are defined differently. These do not represent proper units as elements of the group (U,·). Therefore those special semantic entities are called special units, as opposed to proper units. The set of special units is denoted S, where S ∩ U = {}.    ■2 A special unit s ∈ S is defined as the triple (u, fs, fs-1) where u ∈ U is the “corresponding” proper unit of s and where fs and fs-1 are mutually inverse real functions converting the measurement value to and from the special unit.    ■3 Although not elements of U, special units are said to be “of the same dimension” or “commensurable with” their corresponding proper unit u and the class of units commensurable with u. This can be expressed by means of a binary, symmetric, transitive and reflexive relation ≈ on U ∪ S.

The functions fs and fs-1 are applied as follows: let rs be the numeric measurement value expressed in the special unit s and let m be the corresponding dimensioned quantity, i.e., the measurement with proper unit u. Now, rs = fs(m/u) converts the proper measurement to the special unit and m = fs-1(rs) × u does the inverse.

§22 operations on special units        ■1 In theory, special units cannot take part in any algebraic operations, neither involving other units, nor themselves (exponentiation) nor involving scalars.    ■2 Special units are therefore non-metric units.    ■3 However, due to the requirement of the SI that does allow prefixes on the degree Celsius, special units may be scaled trough a prefix or an arbitrary numeric factor.    ■4 The scale factor α is an additional component of the special unit, which in turn is defined by a quadruple s = (u, fs, fs-1, α). When the functions fs and fs-1 are applied to a measurement value x to convert to and from the special unit the scale factor is applied as follows: x' = fs(x) / α converts from x expressed in the corresponding proper unit to x' in terms of the special unit and x = fs-1(αx') does the reverse.    ■5 Multiplication of a special unit s = (u, fs, fs-1, α) with a scalar β is defined as βs = (u, fs, fs-1, βα). Multiplication of a special unit s with a dimensionless unit r1 is defined as rs.

Since prefixes have a scalar value that multiplies the unit atom, a unit must at least have a defined multiplication operation with a scalar in order to be a candidate for the metric predicate. All proper units are candidates for the metric property, special units are no such candidates.

The Comité Consultatif d'Unités (CCU) decided in February 1995 that any SI prefix may be used with degree Celsius. This statement has not been made explicitly before. This is an unfortunate decision because difference-scale units like the degree Celsius have no multiplication operation, so that the prefix value could be multiplied with the unit. Instead the prefix at non-ratio units scales the measurement value. One wonders why the CGPM keeps the celsius temperature in the SI as it is superfluous and in a unique way incoherent with the SI.

The scale factor α is applied with the functions fs and fs-1 as follows: let rs be the numeric measurement value expressed in the special unit s and let m be the corresponding dimensioned quantity, i.e., the measurement with proper unit u. Now, rs = fs(m/u) / α converts the proper measurement to the special unit and m = fs-1(αrs) × u does the reverse.

§23 definition of special units        ■1 Special units are marked in the definition tables for unit atoms by a bullet (‘•’) in the column titled “value” and a special expression in the column titled “definition”. The BNF for the special expression is `<special-unit> ::= <function-symbol>"("<floating-point-number>" "<term>")"` The function symbols are defined as needed.    ■2 Special expressions are not valid expressions in The Unified Code for Units of Measure, they are only used for defining special units.

## 3.2 Arbitrary Units

§24 arbitrary units        ■1 Arbitrary or procedure defined units are units whose meaning entirely depends on the measurement procedure (assay). These units have no general meaning in relation with any other unit in the SI. Therefore those arbitrary semantic entities are called arbitrary units, as opposed to proper units. The set of arbitrary units is denoted A, where A ∩ U = {}.    ■2 An arbitrary unit has no further definition in the semantic framework of The Unified Code for Units of Measure  ■3 Arbitrary units are not “of any specific dimension” and are not “commensurable with” any other unit.

Until version 1.6 The Unified Code for Units of Measure has dealt with arbitrary units as dimensionless, but as an effect the semantics of The Unified Code for Units of Measure made all arbitrary units commensurable. Since version 1.7 of The Unified Code for Units of Measure it is no longer possible to convert or compare arbitrary units with any other arbitrary unit.

§25 operations on arbitrary units        ■1 Any term involving arbitrary units, is itself an arbitrary unit and is not comparable with any other arbitrary unit or term.

§26 definition of arbitrary units        ■1 Arbitrary units are marked in the definition tables for unit atoms by a bullet (‘•’) in the column titled “value” and a bullet in the column titled “definition”.



[^1]: Interestingly the authors of ENV 12435 forgot to include superscripts in the minimum requirements as given by subclause 7.1.4 for which they do not specify an alternative.

[^2]: A more extensive introduction into this semantics of units can be found in: Schadow G, McDonald CJ et al: Units of Measure in Clinical Information Systems; JAMIA 6(2); Mar/Apr 1999; p. 151–162.

[^3]: See the section about style in §§12ff, to find out how square brackets are actually used. Note, however, that the user has no choice about square bracket symbols, as these are fixed in the list of atomic unit symbols.