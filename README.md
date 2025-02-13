**Table Of Contents**

[1 CREATING AN INSTANCE WITH BECHTLE-VSR AMI](#1-creating-an-instance-with-bechtle-vsr-ami)<br/>
[2 TRY OUR SR SOLUTIONS](#2-try-our-sr-solution)<br/>

---

# 1 Creating an instance with Bechtle-VSR AMI
## PROCEDURE

### Step 1. Choose the AMI we shared
- Click “Launch instance” in EC2 console
- Type "Bechtle-VSR" in the search box and select it.

### Step 2. Choose g4dn.2xlarge instance
choose g4dn.2xlarge
<br/>
<img src="images/aws_choose_g4dn.2xlarge.png" width="70%">
<br/>

### Step 3. Review and launch the instance
- Create a private key if you have no existing key and download it.
<br/>
<img src="images/creating_private_key.png" width="30%">
<br/>
- Click "Launch Instances"

### Step 4. Connect to your instance

```bash
chmod 600 <private_key_path>
ssh -i <private_key_path> ubuntu@<ip_address>
```
Then you can see the following messages:
```

 ____  _____ ____ _   _ _____ _     _____   __     ______  ____  
| __ )| ____/ ___| | | |_   _| |   | ____|  \ \   / / ___||  _ \ 
|  _ \|  _|| |   | |_| | | | | |   |  _| ____\ \ / /\___ \| |_) |
| |_) | |__| |___|  _  | | | | |___| |__|_____\ V /  ___) |  _ < 
|____/|_____\____|_| |_| |_| |_____|_____|     \_/  |____/|_| \_\

                                                  https://blue-dot.io
                                                  contact@blue-dot.io

#### HOWTO ####
bluedot.sh /test-videos/input.mp4 /test-videos/result_x2.mp4 2
bluedot.sh /test-videos/input.mp4 /test-videos/result_x3.mp4 3
```

# 2 Try our SR solution

#### Using easy script(bluedot.sh).
```bash
### 2x SR #######
bluedot.sh /test-videos/input.mp4 /test-videos/result_x2.mp4 2

### 3x SR #######
bluedot.sh /test-videos/input.mp4 /test-videos/result_x3.mp4 3
```

#### Using ffmpeg directly.
```bash
### 2x SR #######
ffmpeg -hide_banner -y -sws_flags spline+accurate_rnd+full_chroma_int -i /test-videos/input.mp4 -vf bdsr_aws=scale=2,scale=out_color_matrix=bt709 -pix_fmt yuv420p -colorspace bt709 -c:v libx264 /test-videos/resutl_x2.mp4

### 3x SR #######
ffmpeg -hide_banner -y -sws_flags spline+accurate_rnd+full_chroma_int -i /test-videos/input.mp4 -vf bdsr_aws=scale=3,scale=out_color_matrix=bt709 -pix_fmt yuv420p -colorspace bt709 -c:v libx264 /test-videos/resutl_x3.mp4
```

