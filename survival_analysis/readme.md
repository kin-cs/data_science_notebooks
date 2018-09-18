

- Survival Analysis (ref: https://www.youtube.com/watch?v=XQfxndJH4UA)
  - python package: **lifelines**
  - Modern Survival Analysis
    - Birth event (e.g. joining the program, join the insurance)
    - Death event (e.g. leaving the program, claim (heavily) for this policy)
    - Probability of surviving
    - For anything we can't capture 'death event', that is censored event.
    - For anything we capture 'death event', we call it uncensored/observed.
      - Survival Curve
        - T: lifetime (death/leave/big claim) of a member of the population
        - t: that time
        - S(t) == P(T > t)
        An example:
        ```python
        from lifelines import KaplanMeierFitter
        kmf = KaplanMeierFitter()
        kmf.fit(T, event_observed=E)  # or, more succiently, kmf.fit(T, E)
        kmf.survival_function_
        kmf.median_
        kmf.plot()
        ```
- Survival Regression
  - e.g. x = (age, crime, smoke,..)
  - S(t|x) = e^{ -H(t|x)}
  - Cox’s Proportional Hazard model
    - example
    ```python
    from lifelines.datasets import load_rossi
    from lifelines import CoxPHFitter

    rossi_dataset = load_rossi()
    cph = CoxPHFitter()
    cph.fit(rossi_dataset, duration_col='week', event_col='arrest', show_progress=True)

    cph.print_summary()  # access the results using cph.summary

    """
    n=432, number of events=114

            coef  exp(coef)  se(coef)       z      p  lower 0.95  upper 0.95
    fin  -0.3790     0.6845    0.1914 -1.9806 0.0476     -0.7542     -0.0039   *
    age  -0.0572     0.9444    0.0220 -2.6042 0.0092     -0.1003     -0.0142  **
    race  0.3141     1.3691    0.3080  1.0198 0.3078     -0.2897      0.9180
    wexp -0.1511     0.8597    0.2121 -0.7124 0.4762     -0.5670      0.2647
    mar  -0.4328     0.6487    0.3818 -1.1335 0.2570     -1.1813      0.3157
    paro -0.0850     0.9185    0.1957 -0.4341 0.6642     -0.4687      0.2988
    prio  0.0911     1.0954    0.0286  3.1824 0.0015      0.0350      0.1472  **
    ---
    Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

    Concordance = 0.640
    Likelihood ratio test = 33.266 on 7 df, p=0.00002
    """
    ```
- **lifelines** package
  - Survival Analysis
  - Survival Regression
  - Statistical test
  - Cross-validation
  - function for transforming lifetables into durations
  - Augmenting data
