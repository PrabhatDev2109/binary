# Binary features for height getting


<?php


echo minheight([4, 8, 10, 12, 14],[8, 4, 12, 10, 14],3);
function minheight($input1,$input2,$input3){
    $n = count($input1);
    $h = 0;
    return getHeight($input1,$input2,0,$n-1,$h,$n);

}

function getHeight($inOrder,$levelOrder,$start,$end,$height,$n){
    
  if($start >$end)
     return 0;

     $getIndex = search($inOrder,$start,$end,$levelOrder[0]);
     if($getIndex == -1)
       return 0;
      
      $leftCount = $getIndex - $start;

      $rightCount = $end - $getIndex;

     
      $newLeftLevel = [];
      for($i=0;$i<$leftCount;$i++){
          $newLeftLevel[$i] = $i;
      }

      $newRightLevel = [ ];
      for($i=0;$i<$rightCount;$i++){
          $newRightLevel[$i] = $i;   
      }  
      
      $lheight = $rheight = $k = 0;

      for($i=0;$i<$n;$i++){
          for($j=$start;$j<$getIndex;$j++){
               if($levelOrder[$i] == $inOrder[$j]){
                   $newLeftLevel[$k] = $levelOrder[$i];
                   $k = $k+1;
                   break;
               }
          }
        }

        $k = 0;
        for($i=0;$i<$n;$i++){
          for($j=$getIndex+1;$j<$end+1;$j++){
               if($levelOrder[$i] == $inOrder[$j]){
                   $newRightLevel[$k] = $levelOrder[$i];
                   $k = $k+1;
                   break;
               }
          }
        }
      
       if($leftCount > 0){
           $lheight = getHeight($inOrder,$newLeftLevel,$start,$getIndex-1,$height,$leftCount);
       }

       if($rightCount > 0){
           $rheight = getHeight($inOrder,$newRightLevel,$getIndex+1,$end,$height,$rightCount);
       }
       $height = max($lheight+1,$rheight+1);
       return $height;

      }



function search($arr,$start,$end,$value){
    
        for($i=$start;$i<$end;$i++){
            
            if($arr[$i] == $value){
               
                return 1;
            }
            
        }
        return -1;
}
