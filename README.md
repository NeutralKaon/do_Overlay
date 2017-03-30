# do_Overlay -- a simple, straightforward colour overlay script in Matlab 

Often, one wants to overlay one image on top of another in Matlab. This is inevitably needlessly difficult. `do_Overlay` is a script that takes at a minimum two arguments: `im_underlay`, and `im_overlay`. These have to have the same in-plane size (i.e. `size(im_underlay,1)==size(im_overlay,1); size(im_underlay,2)==size(im_overlay,2)`). The overlay (colour) image can have a third dimension, which is assumed to be 'time'. A movie will therefore be made (with `pause` statements between each frame to allow for slow video writing). The colour axis is normalised to the max over all time. This is typically used for producing movies of, e.g. contrast agents flashing through a medical imaging reference scan. 

Options are parsed as a struct with a set of sensible defaults, and can contain: 

    hfig -- figure handle for overlay window 
    hax -- axis handle (blank is fine) 
    do_normslice = 1 -- normalise each slice 
    orient =1 -- change to rotate 
    overlay_flag = 'abs' -- function to call on overlayed data
    cmap = 'jet' -- overlay colour scheme 
    bgnd_bright = 0.6 -- brightness of the background [underlay] 
    gamma_background = 0.5 -- gamma adjustment of the background 
    fov_x = 1 -- adjust to crop 
    fov_y = 1 -- adjust to crop 
    zoomFactor = 1.5 -- size of resulting window 
    cutBottom = 0.45 -- bottom of the colour axis (below which is
    transparent)
    cutTop = 1  -- top of the colour axis (above which is red) 
    saveVideo = false -- set to true to save a video 
    videoName = a unique string -- filename 
    overlayString  -- text to write on each video frame 

An example (with somewhat pointless data from the image processing toolbox): 

    underlay = imread('cameraman.tif'); %256x256 greyscale image of a man with a camera
    overlay = imread('circles.png'); %256x256 binary image of circles
    overlay = imfilter(double(overlay),fspecial('gaussian',8,20)); %Blur circles 
    do_Overlay(underlay, overlay); 
    %256x256 RGB image of a man with a camera in B&W with an overlaid set of discs:
    
