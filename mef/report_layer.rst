.. _report_layer:

************
Report Layer
************

Preliminary Discussion
======================

The report layer is populated with constructs to save results of calculations.
These constructs fall into two categories:

- Constructs to tell which software, algorithm(s), and option(s) were used to produce the results
- The results themselves

It is almost impossible and probably not even desirable to normalize fully the report layer.
Tools are very different from one another and produce a wide variety of results.
New calculation methods are regularly proposed.
To normalize everything would lead to a huge and anyway incomplete format.
Moreover, the way results are arranged into reports depends on the study.
It is also, at least to some extent, a matter of taste.

If the Model Exchange Format cannot give a formal structure for the report layer,
it can at least suggest a style to describe
what has been calculated and how it has been calculated.
It can also provide a check-list
of what should be included as information
to make results truly exportable and importable.
The existence of such report style
would be very useful for reporting tools (whether they are graphical or textual):
it would be much easier for these tools to extract the information
they need from the XML result files.

Information about calculations
==============================

Here follows a non-exhaustive list of information
about how the results have been obtained that can be relevant
and other special or unique features of the model.

- Software

    * Version
    * Contact organization (editor, vendor, etc.)
    * ...

- Calculated quantities

    * Name
    * Mathematical definition
    * Approximations used
    * ...

- Calculation method(s)

    * Name
    * Limits (e.g., number of basic events, of sequences, of cut sets)
    * Preprocessing techniques (modularization, rewritings, etc.)
    * Handling of success terms
    * Cutoffs, if any (absolute, relative, dynamic, etc.)
    * Are delete terms, recovery rules or exchange events applied?
    * Extra-logical methods used
    * Secondary software necessary
    * Warning and caveats
    * Calculation time
    * ...

- Features of the model

    * Name
    * Number of: gates, basic events, house events, fault trees, event
      trees, functional events, initiating events

- Feedback

    * Success or failure reports
    * ...

Format of Results
=================

PSA tools produce many kinds of results.
Some are common to most of the tools,
e.g., probability/frequency of some group of consequences, importance factors, sensitivity analyses.
They fall into different categories.
The following three categories are so frequent
that is it worth to normalize the way they are stored into XML files.

- Minimal cut sets (and prime implicants)
- Importance factors
- Statistical measures (with moments)
- Curves

Minimal Cut Sets
----------------

A first (and good) way to encode minimal cut sets
consists in using the representation of formulae defined by the Model Exchange Format.
However, it is often convenient to attach some information to each product,
which is not possible with the formulae of the Model Exchange Format.
An alternative XML representation for sums of products
(sets of minimal cut sets are a specific type of sums of products)
is given in :numref:`schema_sum_of_products`.
More attributes can be added to tags "sum-of-products" and "product"
to carry the relevant information.

.. literalinclude:: schema/sum_of_products.rnc
    :name: schema_sum_of_products
    :caption: The RNC schema for the XML representation of sums-of-products
    :language: rnc

Importance factors
------------------

Importance factors are typically computed for basic events
with the same configurations as for probability analysis.
The following importance factors are long-established and commonly calculated:

    - Fussel-Vesely Diagnosis Importance Factor (DIF)
    - Birnbaum Marginal Importance Factor (MIF)
    - Critical Importance Factor (CIF)
    - Risk Reduction Worth (RRW)
    - Risk Achievement Worth (RAW)

The definitions of these factors can be found in PSA/PRA literature.

In addition to the importance factors,
this report section may contain
the evaluated probability of an event and
the number of products it occurs in.

.. literalinclude:: schema/importance_factors.rnc
    :name: schema_importance_factors
    :caption: The RNC schema for the XML representation of importance factors
    :language: rnc

Statistical measures
--------------------

Statistical measures are typically produced by sensitivity analyses.
They are the result, in general, of Monte-Carlo simulations on the values of some parameter.
Such a measure can come with
moments (mean, standard deviation), confidence ranges, error factors, quantiles, etc.
The XML representation for statistical measure is given in :numref:`schema_statistical_measure`.

.. literalinclude:: schema/statistical_measure.rnc
    :name: schema_statistical_measure
    :caption: The RNC schema for the XML representation of statistical measures
    :language: rnc

Curves
------

Two or three dimensional curves are often produced in PSA studies.
A typical example is indeed
to study the evolution of the system unavailability through the time.
The XML representation of curves suggested by the Model Exchange Format
is given in :numref:`schema_curves`.

.. literalinclude:: schema/curves.rnc
    :name: schema_curves
    :caption: The RNC schema the XML representation of curves
    :language: rnc
