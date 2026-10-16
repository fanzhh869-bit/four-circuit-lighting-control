Classroom lighting commissioning data and code
Release BSERT-CODE-20261016-C18
Related manuscript BSERT-SUBMISSION-20261015-S14

Primary analysis
Observed_Study/data holds the fixed illuminance readings, register endpoints, applied-output logs and instrument settings for classroom R16. The primary endpoints are independent snapshot errors and task classifications, and end-minus-start cumulative electricity on 48 allocated days. State-duration integration is a separate accounting diagnostic. Continuous task-plane lighting quality was not recorded on those days.

Quick start from Repository with Python 3.12
python -m pip install -r requirements.txt
python run_study.py info
python run_study.py check-files
python run_study.py verify
python run_study.py analyse --destination ../observed_analysis_output
python run_study.py draw --destination ../main_figure_output
Analysis and drawing require new destinations outside Repository. NumPy 2.3.5 supports analysis; drawing additionally requires Matplotlib 3.11.2 and installed Times New Roman. Font files are not distributed.

Analysis interfaces
observed_analysis.py fits responses and analyses meter records. mechanism_analysis.py derives snapshot decision matrices, 45 request/background combinations and recorded-output accounting. execution_eligible identifies records suitable for output diagnostics; actual_day_eligible separately identifies eligible register outcomes. Local applied outputs are recorded without independent continuous lamp feedback. Regression uses the recorded FZ12, P8, P12 and P24 labels directly.

Separate numerical analyses
Model_Study contains optical parameter comparisons, common-input policy replays and sensitivity calculations. Its numerical units and assumptions are described in its README and the model supplement.
python run_study.py summarise-model --destination ../model_summary_output
To reproduce the full numerical project, install Model_Study/requirements_all.txt and run:
python run_study.py model-reproduce --workers 4 --destination ../model_analysis_output
These calculations are separate from the primary observation entry point.

Data navigation
Observed_Study/results: primary spatial, metered and diagnostic results.
Observed_Study/data/Figure_01.png and Figure_01.tif: the shared hardware figure.
Observed_Study/figures: PNG previews of the six plotted main figures. The drawing command regenerates EPS, SVG, PDF and PNG exports in a fresh destination.
Model_Study/mechanism_results: controlled numerical summaries.
documentation/publication_output_map.csv: sources for all 76 publication figures and tables.
documentation/observation_input_origin_map.csv: field-level archive extraction paths and hashes. Shared input files have one stored copy. Model_Study/Study/input_storage_map.json maps numerical input names to those copies; the numerical runner stages them into an isolated working directory. Storage location is distinct from analytical role.
documentation/primary_data_dictionary.csv: result fields, units and roles.
documentation/code_inventory.csv: primary source dependencies and hashes.
validation: current analysis verification and file-consistency checks.
Input values and raw log identifiers are retained. Boot identifiers distinguish recorded log sessions; software and protocol identifiers are not acquisition dates.

Authors
Zhongshuai Li, Yue Song, Yuxin Yan, Zhenhua Fan, Nanjie Zhou, Longhang Zhou, Zhejie Meng.
School of Energy and Power Engineering, Changchun Institute of Technology, Changchun 130012, China.
Corresponding author: Yue Song; yue_song@live.cn; https://orcid.org/0009-0008-7104-5368.
Funding, repository address and licence selection await author completion.

Assistance
OpenAI Codex assisted drafting, translation, code development and data visualisation. Archived verification routines check analysis outputs.

Dictionary fields
CSV fields are column names and NPZ fields are array keys. Nested JSON fields use paths such as $[*]["lamp_coefficients"]. Wildcards select list records. Each path is verified against its source. From Repository, reproduce the dictionary with python documentation/build_data_dictionary.py --destination ../primary_data_dictionary.csv. Example outputs are siblings of Repository and must not already exist. The daylight_reference_lxh field is an illuminance-time integral in lx h.
