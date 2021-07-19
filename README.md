# SFND Radar Target Generation and Detection

## Implementation steps for the 2D CFAR process.
 - first, set the number of the training cells and guard cells for each domain (range domain and Doppler domain).
 - then, offset the threshold by SNR value in dB, create a vector to store noise_level for each iteration on training cells
 - Finally, I create a loop that extract only the Training cells. To do that, I first get the sliding patch and, after converting it to power from decibel, then I set to zero whatever it is not in the position of training cells; the zero submatrix will not contribute to the sum over the whole patch and, by dividing for the number of training cells I will get the noise mean level.

## Selection of Training, Guard cells and offset.
```MATLAB
%Select the number of Training Cells in both the dimensions.
Tr = 10;
Td = 5;
% *%TODO* :
%Select the number of Guard Cells in both dimensions around the Cell under
%test (CUT) for accurate estimation
Gr = 5;
Gd = 5;
```

## Steps taken to suppress the non-thresholded cells at the edges.
```
if RDM(i+(Td+Gd),j+(Td+Gr))>sigThresh
    CFAR_sig(i+(Td+Gd),j+(Td+Gr)) = 1;
else
    CFAR_sig(i+(Td+Gd),j+(Td+Gr)) = 0;
end
```
