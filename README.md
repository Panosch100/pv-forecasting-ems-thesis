# pv-forecasting-ems-thesis
Diploma thesis code:Development of an Energy Management System using Forecasting Models for Photovoltaic Facilities

# Ανάπτυξη Συστήματος Διαχείρισης Ενέργειας μέσω Μοντέλων Πρόβλεψης για Φωτοβολταϊκές Εγκαταστάσεις

Κώδικας διπλωματικής εργασίας.

**Συγγραφέας:** Παναγιώτης Χαΐδας (ΑΕΜ 03399)
**Επιβλέπουσα:** Ελένη Τουσίδου
**Τμήμα:** Ηλεκτρολόγων Μηχανικών και Μηχανικών Υπολογιστών, Πανεπιστήμιο Θεσσαλίας
**Έτος:** 2026

## Περιεχόμενο

Η εργασία αναπτύσσει μοντέλα μηχανικής και βαθιάς μάθησης για την
πρόβλεψη φωτοβολταϊκής παραγωγής και ηλεκτρικού φορτίου, και τα
ενσωματώνει σε σύστημα διαχείρισης ενέργειας βασισμένο σε κανόνες.
Η αξιολόγηση γίνεται στο μικροδίκτυο DKP του Desert Knowledge Australia
Solar Centre στο Alice Springs.

Τρία επίπεδα ανάλυσης:

1. Πρόβλεψη σε επίπεδο συστοιχίας (M9, Trina 23.4 kW), με αναπαραγωγή
   της μεθοδολογίας των Singh, Saraswat και Gupta (Next Energy, 2026)
2. Πρόβλεψη σε επίπεδο μικροδικτύου, σε δύο ορίζοντες: 5 λεπτά και
   προημερήσιος
3. Προσομοίωση συστήματος διαχείρισης ενέργειας με μπαταρία 358 kWh,
   σε τέσσερα σενάρια

## Δομή

| Φάκελος | Περιεχόμενο |
|---|---|
| `panel_level/` | Πρόβλεψη συστοιχίας M9 |
| `microgrid_pv/` | Πρόβλεψη φωτοβολταϊκής παραγωγής μικροδικτύου |
| `microgrid_load/` | Πρόβλεψη φορτίου μικροδικτύου |
| `ems/` | Προσομοίωση συστήματος διαχείρισης ενέργειας |
| `eda/` | Διερευνητική ανάλυση δεδομένων |
| `results/` | Μετρικές αξιολόγησης σε μορφή JSON |
| `predictions/` | Προβλέψεις μοντέλων σε μορφή CSV |

## Notebooks

| Αρχείο | Μοντέλα |
|---|---|
| `panel_level/PV_Forecasting_CPU_M9.ipynb` | XGBoost, Random Forest, SVR |
| `panel_level/PV_Forecasting_GPU_M9.ipynb` | Stacked LSTM, 1D-CNN, CNN-LSTM, Bi-LSTM |
| `microgrid_pv/PV_Microgrid_Forecasting_CPU.ipynb` | XGBoost, Random Forest, SVR, persistence |
| `microgrid_pv/PV_Microgrid_Forecasting_GPU.ipynb` | Stacked LSTM, CNN-LSTM, Bi-LSTM, encoder-decoder |
| `microgrid_load/Load_Forecasting_CPU.ipynb` | XGBoost, Random Forest, SVR, persistence |
| `microgrid_load/Load_Forecasting_GPU.ipynb` | Stacked LSTM, CNN-LSTM, Bi-LSTM, encoder-decoder |
| `ems/EMS_RULEBASED.ipynb` | Προσομοίωση τεσσάρων σεναρίων |
| `eda/EDA_Analysis.ipynb` | Στατιστική ανάλυση και συσχετίσεις |
| `eda/DKP_MICROGRID_INFO.ipynb` | Χαρακτηριστικά της εγκατάστασης |

## Δεδομένα

Τα δεδομένα προέρχονται από το Desert Knowledge Australia Solar Centre
και δεν περιλαμβάνονται στο αποθετήριο λόγω μεγέθους. Κατεβαίνουν
ελεύθερα από το https://dkasolarcentre.com.au/download

| Αρχείο | Περιγραφή |
|---|---|
| `87-Site_DKA-M9_A+C-Phases.csv` | Συστοιχία M9 (Trina, 23.4 kW) |
| `239-Site_DKA_Totals-BESS.csv` | Σύστημα αποθήκευσης |
| `240-Site_DKA_Totals-Site_Demand.csv` | Ζήτηση εγκατάστασης |
| `241-Site_DKA_Totals-PV.csv` | Συνολική φωτοβολταϊκή παραγωγή |
| `242-Site_DKA_Totals-Grid.csv` | Ανταλλαγή με το δίκτυο |

## Εκτέλεση

Τα notebooks γράφτηκαν για Google Colab με προσαρτημένο Google Drive.
Η διαδρομή των δεδομένων ορίζεται στα πρώτα κελιά κάθε notebook και
πρέπει να προσαρμοστεί στο δικό σας περιβάλλον.

Τα notebooks με κατάληξη GPU απαιτούν επιταχυντή. Στο Colab:
Runtime, Change runtime type, T4 GPU.

Βιβλιοθήκες: pandas, numpy, scikit-learn, xgboost, tensorflow,
matplotlib, seaborn, requests.

## Σειρά εκτέλεσης

1. `eda/EDA_Analysis.ipynb`
2. `panel_level/` και στη συνέχεια `microgrid_pv/`, `microgrid_load/`
3. `ems/EMS_RULEBASED.ipynb`, που διαβάζει τα αρχεία του `predictions/`

## Σημείωση

Τα εκπαιδευμένα μοντέλα δεν περιλαμβάνονται, καθώς ξεπερνούν τα όρια
μεγέθους του GitHub. Αναπαράγονται εκτελώντας τα αντίστοιχα notebooks.
