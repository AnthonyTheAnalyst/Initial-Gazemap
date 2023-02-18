# Initial-Gazemap

This code creates a simple gazemap overlay over a video using x, y and ms data points. 
The video output that this provides will have a white border which I subsequently used to add info about the GazeMap. 


This is an early sample of a project that was later used to create a proprietary heatmap. 

The data that was used for this project was derived from getting eyetracking data from multiple data sources. 
All data sources were eventually converged into seperate csv files containing 3 columns (x-coordinates, y-coordinates, ms). 

The code is built off of those parameters. If you're data is different you'll have to adjust this section to feed the program the correct data. 

def read_text_file(file_path):
    with open(file_path,'r') as f:
        df = pd.read_csv(f)
        xc = df['GazeX']
        yc = df['GazeY']
        msc = df['ms']
        x_coords.append(xc)
        y_coords.append(yc)
        ms_time.append(msc)
        f.close()
        # print(len(x_coords),len(y_coords),len(ms_time))

#iterating through the folder 
for file in os.listdir():
    #check whether file is in csv format or not
    if file.endswith(".csv"):
        file_path = f"{path}\{file}"
        #call read file function
        read_text_file(file_path)


for n in range(len(ms_time)):
    x = np.append(x,x_coords[n])
    y = np.append(y,y_coords[n])
    ms = np.append(ms,ms_time[n])
    
t=[]

for i in range(len(x)):
    ms_temp=ms[i]
    x_temp=x[i]
    y_temp=y[i]
    data = [ms_temp,x_temp,y_temp]
    t.append(data)

#need to handle nans before I create the df 
arr = np.array(t)

column_values = ['ms','GazeX','GazeY']
df = pd.DataFrame(data = arr, columns=column_values)
df = df.sort_values(by=['ms'])
df.reset_index(drop=True,inplace=True)

###This is to get rid of your NaNs in the data#####
bad = []

for i in range(len(df)):
    try:
        int(df.GazeX[i])
    except ValueError:
        bad.append(i)
        
if bad == []:
    pass
else:
    df = df.drop(labels = bad,axis=0)
    df.reset_index(drop=True,inplace=True)

bad = []

for i in range(len(df)):
    try:
        int(df.GazeY[i])
    except ValueError:
        bad.append(i)

if bad == []:
    pass
else:
    df = df.drop(labels = bad,axis=0)
    df.reset_index(drop=True,inplace=True)
    
   
 The actual plotting of points and aligning them to a video starts on line 132 of this code. 
    
 I hope this helps someone!
