# See: http://omino.com/sw/qt_tools/
if [[ -x `which qt_export` ]]; then
  create_image_mov() {
    if [[ $# = 0 ]]
    then
      echo "Usage:     $0 image_name move_name"
      echo "Create movie using png compression."
      echo "Example:   $0 watershed_01.png (outputs watershed.mov)"
      echo "Example:   $0 watershed_01.png out.mov (outputs out.mov)"
    else
      if [[ $# > 1 ]]
      then
        out=$2
      else
        out=$(echo $aa:r | sed 's/_*[0-9]*//g').mov 
      fi
      qt_export --sequencerate=1 $1 --video=png,1 --audio=0 --replacefile $out
    fi
  }
fi

if [[ -x `which mencoder` ]]; then
  function mkv_to_avi(){
      # Remux .mkv or .ogm to .avi with mp3 audio.
      input=''
      output=${input:r}.avi
      mencoder $input -oac mp3lame -ovc copy -o $output
  }

  function mkv_to_avi(){
      # Convert .mkv or .ogm to .avi with XViD and mp3 audio.
      input=''
      output=${input:r}.avi
      mencoder $input -oac mp3lame -ovc xvid -xvidencopts pass=1 -o $output
  }
fi