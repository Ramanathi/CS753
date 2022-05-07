# CS753
## Files edited
* compatibale to CPUs : the part with `to('cuda')` is edited out
* new command line argument : it is introduced to test max and mean pooling - `pool_mode`
* pooling in *nets/net_audiovisual.py* : (line 127 through 135) 
![image](https://user-images.githubusercontent.com/55206019/167242263-b275c18a-d7a3-42c5-8c5e-7e369604d54c.png)
## New Files Generated
Two models namely MMIL_Net_max.pt and MMIL_Net.mean.pt are generated in *models/* folder with the above changes
## Generating the Results
`$ python hacker/AVVP-ECCV20-master/main_avvp.py --mode train --pool_mode att --checkpoint MMIL_Net --audio_dir hacker/feats/vggish/ --video_dir hacker/feats/res152/ --st_dir hacker/feats/r2plus1d_18/` <br />
* For attention model use pool_mode as "att". Use "mean" and "max" in case of mean pooling and max pooling respectively
* Generated F1 scores are presented in *results* file
## Two variations of max pooling
* pick one snippet for one category
    * After multiplication of Wtp, p, Wav for every category, sum up audio and visual probailities to get 10 real valued vector and assign p to the maximum value among them
    * Every Category may have different snippets choosen i.e. for example "speech" category may have picked t = 3 and "dog" category would pick t = 9
* pick the same one snippet for every category
    * compute 10 valued vector as before for every category and compute variance of every snippet among all categories and pick the snippet which has least variance
    * every category would choose same snippet
