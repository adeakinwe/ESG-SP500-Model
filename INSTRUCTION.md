unalias python
conda activate xgb214  

conda install --file requirements.txt 

conda list -n xgb214 shap

python -c "import xgboost; print(xgboost.__version__)"