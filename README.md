# job-sql-improvement
Optimizing the SQL query for better performance
## Given script:
```sql
SELECT Jobs.id AS `Jobs__id`,
Jobs.name AS `Jobs__name`,
Jobs.media_id AS `Jobs__media_id`,
Jobs.job_category_id AS `Jobs__job_category_id`,
Jobs.job_type_id AS `Jobs__job_type_id`,
Jobs.description AS `Jobs__description`,
Jobs.detail AS `Jobs__detail`,
Jobs.business_skill AS `Jobs__business_skill`,
Jobs.knowledge AS `Jobs__knowledge`,
Jobs.location AS `Jobs__location`,
Jobs.activity AS `Jobs__activity`,
Jobs.academic_degree_doctor AS `Jobs__academic_degree_doctor`,
Jobs.academic_degree_master AS `Jobs__academic_degree_master`,
Jobs.academic_degree_professional AS `Jobs__academic_degree_professional`,
Jobs.academic_degree_bachelor AS `Jobs__academic_degree_bachelor`,
Jobs.salary_statistic_group AS `Jobs__salary_statistic_group`,
Jobs.salary_range_first_year AS `Jobs__salary_range_first_year`,
Jobs.salary_range_average AS `Jobs__salary_range_average`,
Jobs.salary_range_remarks AS `Jobs__salary_range_remarks`,
Jobs.restriction AS `Jobs__restriction`,
Jobs.estimated_total_workers AS `Jobs__estimated_total_workers`,
Jobs.remarks AS `Jobs__remarks`,
Jobs.url AS `Jobs__url`,
Jobs.seo_description AS `Jobs__seo_description`,
Jobs.seo_keywords AS `Jobs__seo_keywords`,
Jobs.sort_order AS `Jobs__sort_order`,
Jobs.publish_status AS `Jobs__publish_status`,
Jobs.version AS `Jobs__version`,
Jobs.created_by AS `Jobs__created_by`,
Jobs.created AS `Jobs__created`,
Jobs.modified AS `Jobs__modified`,
Jobs.deleted AS `Jobs__deleted`,
JobCategories.id AS `JobCategories__id`,
JobCategories.name AS `JobCategories__name`,
JobCategories.sort_order AS `JobCategories__sort_order`,
JobCategories.created_by AS `JobCategories__created_by`,
JobCategories.created AS `JobCategories__created`,
JobCategories.modified AS `JobCategories__modified`,
JobCategories.deleted AS `JobCategories__deleted`,
JobTypes.id AS `JobTypes__id`,
JobTypes.name AS `JobTypes__name`,
JobTypes.job_category_id AS `JobTypes__job_category_id`,
JobTypes.sort_order AS `JobTypes__sort_order`,
JobTypes.created_by AS `JobTypes__created_by`,
JobTypes.created AS `JobTypes__created`,
JobTypes.modified AS `JobTypes__modified`,
JobTypes.deleted AS `JobTypes__deleted`
FROM jobs Jobs
LEFT JOIN jobs_personalities JobsPersonalities
ON Jobs.id = (JobsPersonalities.job_id)
LEFT JOIN personalities Personalities
ON (Personalities.id = (JobsPersonalities.personality_id)
AND (Personalities.deleted) IS NULL)
LEFT JOIN jobs_practical_skills JobsPracticalSkills
ON Jobs.id = (JobsPracticalSkills.job_id)
LEFT JOIN practical_skills PracticalSkills
ON (PracticalSkills.id = (JobsPracticalSkills.practical_skill_id)
AND (PracticalSkills.deleted) IS NULL)
LEFT JOIN jobs_basic_abilities JobsBasicAbilities
ON Jobs.id = (JobsBasicAbilities.job_id)
LEFT JOIN basic_abilities BasicAbilities
ON (BasicAbilities.id = (JobsBasicAbilities.basic_ability_id)
AND (BasicAbilities.deleted) IS NULL)
LEFT JOIN jobs_tools JobsTools
ON Jobs.id = (JobsTools.job_id)
LEFT JOIN affiliates Tools
ON (Tools.type = 1
AND Tools.id = (JobsTools.affiliate_id)
AND (Tools.deleted) IS NULL)
LEFT JOIN jobs_career_paths JobsCareerPaths
ON Jobs.id = (JobsCareerPaths.job_id)
LEFT JOIN affiliates CareerPaths
ON (CareerPaths.type = 3
AND CareerPaths.id = (JobsCareerPaths.affiliate_id)
AND (CareerPaths.deleted) IS NULL)
LEFT JOIN jobs_rec_qualifications JobsRecQualifications
ON Jobs.id = (JobsRecQualifications.job_id)
LEFT JOIN affiliates RecQualifications
ON (RecQualifications.type = 2
AND RecQualifications.id = (JobsRecQualifications.affiliate_id)
AND (RecQualifications.deleted) IS NULL)
LEFT JOIN jobs_req_qualifications JobsReqQualifications
ON Jobs.id = (JobsReqQualifications.job_id)
LEFT JOIN affiliates ReqQualifications
ON (ReqQualifications.type = 2
AND ReqQualifications.id = (JobsReqQualifications.affiliate_id)
AND (ReqQualifications.deleted) IS NULL)
INNER JOIN job_categories JobCategories
ON (JobCategories.id = (Jobs.job_category_id)
AND (JobCategories.deleted) IS NULL)
INNER JOIN job_types JobTypes
ON (JobTypes.id = (Jobs.job_type_id)
AND (JobTypes.deleted) IS NULL)
WHERE ((JobCategories.name LIKE ' %キャビンアテンダント% '
OR JobTypes.name LIKE ' %キャビンアテンダント% '
OR Jobs.name LIKE ' %キャビンアテンダント% '
OR Jobs.description LIKE ' %キャビンアテンダント% '
OR Jobs.detail LIKE ' %キャビンアテンダント% '
OR Jobs.business_skill LIKE ' %キャビンアテンダント% '
OR Jobs.knowledge LIKE ' %キャビンアテンダント% '
OR Jobs.location LIKE ' %キャビンアテンダント% '
OR Jobs.activity LIKE ' %キャビンアテンダント% '
OR Jobs.salary_statistic_group LIKE ' %キャビンアテンダント% '
OR Jobs.salary_range_remarks LIKE ' %キャビンアテンダント% '
OR Jobs.restriction LIKE ' %キャビンアテンダント% '
OR Jobs.remarks LIKE ' %キャビンアテンダント% '
OR Personalities.name LIKE ' %キャビンアテンダント% '
OR PracticalSkills.name LIKE ' %キャビンアテンダント% '
OR BasicAbilities.name LIKE ' %キャビンアテンダント% '
OR Tools.name LIKE ' %キャビンアテンダント% '
OR CareerPaths.name LIKE ' %キャビンアテンダント% '
OR RecQualifications.name LIKE ' %キャビンアテンダント% '
OR ReqQualifications.name LIKE ' %キャビンアテンダント% ')
AND publish_status = 1
AND (Jobs.deleted) IS NULL)
GROUP BY Jobs.id
ORDER BY Jobs.sort_order desc,
Jobs.id DESC LIMIT 50 OFFSET 0
```
## Tables involved
    1. Jobs (main tables)
    2. JobsPersonalities
    3. Personalities
    4. JobsPracticalSkills
    5. PracticalSkills
    6. JobsBasicAbilities
    7. BasicAbilities
    8. JobsTools
    9. JobsCareerPaths
    10. JobsRecQualifications
    11. JobsReqQualifications
    12. JobCategories
    13. JobTypes

## What this SQL trying to achieve:
- this SQL is trying to retrieves job-related information from database while performing multiple LEFT JOINs and INNER JOINs with various tables.
- the query filters The query filters results based on a Japanese keyword "キャビンアテンダント".
- it also ensures that only active, non-deleted jobs are included.

## Script breakdown
1. Job Data selection:
    - The SELECT statement retrieves details from the `Jobs` table.
    - Related data from `job_categories` and `job_types` tables.

2. Joining Related Tables:
    - Personality Traits (jobs_personalities, personalities)
    - Practical Skills (jobs_practical_skills, practical_skills)
    - Basic Abilities (jobs_basic_abilities, basic_abilities)
    - Tools (jobs_tools, affiliates with `type = 1`)
    - Career Paths (jobs_career_paths, affiliates with `type = 3`)
    - Recommended Qualifications (jobs_rec_qualifications, affiliates with `type = 2`)
    - Required Qualifications (jobs_req_qualifications, affiliates with `type = 2`)
    - `INNER JOIN` job_categories and `INNER JOIN` job_types ensure that the job category and type are mandatory (for example: a job must have a valid category and type).

3. Filtering (`WHERE` function)
     - to search keyword "キャビンアテンダント" in multiple fields across different tables (for instance: job name, description, skills, qualifications, etc.)
     - to find only published job `publish_status = 1`.
     - to exclude deleted jobs `Jobs.deleted IS NULL`.

4. Grouping and sorting
    - `GROUP BY Jobs.id`: Groups results by job ID
    - `ORDER BY Jobs.sort_order DESC, Jobs.id DESC` : Prioritizes jobs based on `sort_order` (descending) and then by `job ID` (latest jobs first).

5. Pagination:
    - `limit 50 offset 0` retrived only 50 matching results.

## Issues
- overused `LEFT JOIN`s and affiliates tables.
- usage of `LIKE '%キャビンアテンダント%'` will slow the performance.
- Unnecessary Grouping; there is a groupby query but no aggregate functions like COUNT(), SUM() etc are used.

## Improvised Script
```sql
SELECT Jobs.id AS Jobs__id,
       Jobs.name AS Jobs__name,
       Jobs.description AS Jobs__description,
       Jobs.job_category_id AS Jobs__job_category_id,
       Jobs.job_type_id AS Jobs__job_type_id,
       Jobs.salary_range_first_year AS Jobs__salary_range_first_year,
       Jobs.salary_range_average AS Jobs__salary_range_average,
       Jobs.publish_status AS Jobs__publish_status,
       Jobs.sort_order AS Jobs__sort_order,
       Jobs.created AS Jobs__created,
       JobCategories.name AS JobCategories__name,
       JobTypes.name AS JobTypes__name
FROM jobs Jobs
INNER JOIN job_categories JobCategories ON JobCategories.id = Jobs.job_category_id AND JobCategories.deleted IS NULL
INNER JOIN job_types JobTypes ON JobTypes.id = Jobs.job_type_id AND JobTypes.deleted IS NULL
LEFT JOIN jobs_personalities JobsPersonalities ON Jobs.id = JobsPersonalities.job_id
LEFT JOIN personalities Personalities ON Personalities.id = JobsPersonalities.personality_id AND Personalities.deleted IS NULL
LEFT JOIN jobs_practical_skills JobsPracticalSkills ON Jobs.id = JobsPracticalSkills.job_id
LEFT JOIN practical_skills PracticalSkills ON PracticalSkills.id = JobsPracticalSkills.practical_skill_id AND PracticalSkills.deleted IS NULL
LEFT JOIN jobs_basic_abilities JobsBasicAbilities ON Jobs.id = JobsBasicAbilities.job_id
LEFT JOIN basic_abilities BasicAbilities ON BasicAbilities.id = JobsBasicAbilities.basic_ability_id AND BasicAbilities.deleted IS NULL
LEFT JOIN jobs_tools JobsTools ON Jobs.id = JobsTools.job_id
LEFT JOIN (
    SELECT id, name FROM affiliates WHERE type = 1 AND deleted IS NULL
) Tools ON Tools.id = JobsTools.affiliate_id
LEFT JOIN jobs_career_paths JobsCareerPaths ON Jobs.id = JobsCareerPaths.job_id
LEFT JOIN (
    SELECT id, name FROM affiliates WHERE type = 3 AND deleted IS NULL
) CareerPaths ON CareerPaths.id = JobsCareerPaths.affiliate_id
LEFT JOIN jobs_rec_qualifications JobsRecQualifications ON Jobs.id = JobsRecQualifications.job_id
LEFT JOIN (
    SELECT id, name FROM affiliates WHERE type = 2 AND deleted IS NULL
) RecQualifications ON RecQualifications.id = JobsRecQualifications.affiliate_id
LEFT JOIN jobs_req_qualifications JobsReqQualifications ON Jobs.id = JobsReqQualifications.job_id
LEFT JOIN (
    SELECT id, name FROM affiliates WHERE type = 2 AND deleted IS NULL
) ReqQualifications ON ReqQualifications.id = JobsReqQualifications.affiliate_id
WHERE MATCH(Jobs.name, Jobs.description, Jobs.detail, Jobs.business_skill, Jobs.knowledge)
AGAINST ('キャビンアテンダント' IN NATURAL LANGUAGE MODE)
AND Jobs.publish_status = 1
AND Jobs.deleted IS NULL
ORDER BY Jobs.sort_order DESC, Jobs.created DESC
LIMIT 50 OFFSET 0;
```

## Key improvement:
 1. Use `INNER JOIN` instead of `LEFT JOIN` for `affiliates` when the data is required.
Pre-filter affiliates before joining using subqueries to avoid unnecessary joins; This reduces the size of the joined dataset.
 2. Execute pre-filtering.
 example:
 ```sql
 -- prefilter affiliates for type = 1 in Tools
 LEFT JOIN (
    SELECT id, name FROM affiliates WHERE type = 1 AND deleted IS NULL
) Tools ON Tools.id = JobsTools.affiliate_id
 -- prefilter affiliates for type = 3 in carrerPaths
LEFT JOIN (
    SELECT id, name FROM affiliates WHERE type = 3 AND deleted IS NULL
) CareerPaths ON CareerPaths.id = JobsCareerPaths.affiliate_id
 -- prefilter affiliates for type = 2 in RecQualifications
LEFT JOIN (
    SELECT id, name FROM affiliates WHERE type = 2 AND deleted IS NULL
) RecQualifications ON RecQualifications.id = JobsRecQualifications.affiliate_id
 -- prefilter affiliates for type = 2 in ReqQualifications
LEFT JOIN (
    SELECT id, name FROM affiliates WHERE type = 2 AND deleted IS NULL
) ReqQualifications ON ReqQualifications.id = JobsReqQualifications.affiliate_id
 ```
 3. using Match(...) AGAINST ('キャビンアテンダント' IN NATURAL LANGUAGE MODE) for word filtering.
    - Enable ngram parser to properly tokenize Japanese text (this is in the MYSQL config file; if you are using mysql older version than 8.0; you need an upgrade).

 ## Key Benefits
- Faster Execution: Reduces unnecessary joins, and grouping
- Better Search: Full-text search (MATCH ... AGAINST) for Japanese characters.

## Time Spent
- understanding and analyzing the script (90 - 120 minutes)
- testing and refining (60-90 minutes)
- Final Adjustments and Documentation (30-60 minutes)
