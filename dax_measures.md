// =====================================================================
// SANITORAL PROJECT PORTFOLIO - CORE DAX MEASURES
// Table: Measures
// =====================================================================

// --- 1. BASELINE & ACTUAL AGGREGATIONS ---

[Planned Cost] = 
SUM('Projects_plans'[Planned_Cost])

[Actual Cost] = 
SUM('Actual_Costs'[Actual_Cost])

[Planned Duration] = 
SUM('Projects_plans'[Planned_Duration])

[Actual Duration] = 
SUM('Actual_Duration'[Actual_Duration])

[Planned Deliverables] = 
SUM('Projects_plans'[Planned_Deliverable])

[Actual Deliverables] = 
SUM('Actual_Deliverable'[Actual_Deliverables])


// --- 2. VARIANCE ANALYSIS (ABSOLUTE & PERCENTAGE) ---

[Cost Variance] = 
[Actual Cost] - [Planned Cost]

[Cost Variance %] = 
DIVIDE([Cost Variance], [Planned Cost], 0)

[Duration Variance] = 
[Actual Duration] - [Planned Duration]

[Duration Variance %] = 
DIVIDE([Duration Variance], [Planned Duration], 0)

[Deliverables Variance] = 
[Actual Deliverables] - [Planned Deliverables]

[Deliverables Variance %] = 
DIVIDE([Deliverables Variance], [Planned Deliverables], 0)


// --- 3. GOVERNANCE & ALERT SYSTEM (>= 15% DRIFT) ---

[Project on Alert] = 
IF(
    [Cost Variance %] >= 0.15 || [Duration Variance %] >= 0.15 || [Deliverables Variance %] <= -0.15,
    1,
    0
)

[Total Projects Count] = 
DISTINCTCOUNT('Projects_plans'[Project ID])

[Alerted Projects Count] = 
CALCULATE(
    [Total Projects Count],
    FILTER('Projects_plans', [Project on Alert] = 1)
)