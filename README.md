# lefse
cd /data/valenzur/Shukla_microbiome_seq/

cd qiime2

cd mc_followup

cp metagenome_predictions_L3.q2.txt ~/software/

cd ~/software/humann-0.99/

cd /data/valenzur/Shukla_microbiome_seq/mc_followup

cp Shukla_MC_ABLV_mapping.txt ~/software/

tail -n +2 Shukla_MC_ABLV_mapping.txt | awk '{ print $1 }' | sed 's/_/ /g' | awk '{ print $1""$2""$3" "$3 }' > osrp.mapping.sample.id.class.txt

awk -F "\t" 'FNR==NR{a[$1]=$0; next}$1 in a {print a[$1]}' osrp.mapping.sample.id.class.txt osrp.sample.id.order.txt | head

sed 's/A/ A/g' osrp.sample.id.order.txt | sed 's/B/ B/g' | sed 's/L/ L/g' | sed 's/V/ V/g' | awk '{ print $2 }' | awk 'BEGIN { ORS = "\t" }{print}' > osrp.classes.ordered.row.txt

vim osrp.classes.ordered.row.txt

cat osrp.classes.ordered.row.txt metagenome_predictions_L3.q2.txt > metagenome_predictions_L3.q2_edited.txt

vim metagenome_predictions_L3.q2_edited.txt

less -S metagenome_predictions_L3.q2.txt

cd ~/software/

rev metagenome_predictions_L3.q2.txt | cut -f2- | rev | sed 's/ /_/g' > metagenome_predictions_L3.q2.edited.txt

cat osrp.classes.ordered.row.txt metagenome_predictions_L3.q2.edited.txt > metagenome_predictions_L3.q2.edited2.txt

vim metagenome_predictions_L3.q2.edited2.txt

/home/valenzur/software/nsegata-lefse-82605a2ae7b7/format_input.py metagenome_predictions_L3.q2.edited2.txt metagenome_predictions_L3.q2.edited2.4lefse.u4.lefse -c 1 -u 4

/home/valenzur/software/nsegata-lefse-82605a2ae7b7/run_lefse.py  metagenome_predictions_L3.q2.edited2.4lefse.u4.lefse shed.picrust.humann.4lefse.u4.lefse.out -l 4

miniconda2/bin/lefse-plot_res.py --dpi 300 shed.picrust.humann.4lefse.u4.lefse.out shed.picrust.humann.4lefse.u4.lefse.out.png





