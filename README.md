# jsp
 project-backup file using shellscript

 #!?bin/bash

src_dir=/home/ubuntu/shellscript
tgt_dir=/home/ubuntu/backup

curr_timestamp=$(date "+%Y-%m-%d-%H-%M-%S")
backup_file=$tgt_dir/$curr_timestamp.tgz

echo " Taking backup on $curr_timestamp"
echo "$backup_file"

tar czf $backup_file --absolute-names $src_dir

echo "Backup complete"



project-check disk usage using shellscript

#!/bin/bash

alert=20
backup_date=$(date +'%m/%d/%Y %H:%M:%S')
df -H | awk '{print $5 " " $1}' | while read output;
do
  echo "Disk Detail: $output"
  usage=$(echo $output | awk '{print $1}' | cut -d'%' -f1)
  file_sys=$(echo $output | awk '{print $2}')
  
  if [ $usage -ge $alert ]
 then
    echo "CRITICAL for $file_sys on $backup_date"
  fi  
done 
