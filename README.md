# MultiThreadingPython
## Ikjot Singh
## 102116071
## 3CS11

### Methodology
- Import necessary libraries
- Created a function to generate random matrices of order 1000*1000
```
def random_matrix():
    return np.random.rand(1000, 1000)
x=random_matrix()
```

- Created a constant matrix of the same order
```
y = np.eye(1000)
y=y*2
```

- Created the task function that multiplies matrices
```
def multiply_matrix():
    print(np.dot(random_matrix(), y))
    return np.dot(random_matrix(), y)
```

- Created a parametrized function for threading
```
def threadfn(numberOfThreads):
  startTime = time.time()
  activeThreads = threading.active_count()
  print("Program Started....")
  for i in range(100):
      t = threading.Thread(target=random_matrix)
      t.start()
      while True:
        if threading.active_count() - activeThreads + 1 <= numberOfThreads:
          break
        time.sleep(1)

  while True:
      if threading.active_count() == activeThreads:
          break
      else:
          print ("Thread still running (left %d)..."%(threading.active_count() - activeThreads))
          time.sleep(1)
    
  print("All Thread ends")

  print("Program Finished")
  print("Total Time %f sec" % (round( time.time() - startTime,4)))
  x=round( time.time() - startTime,4)
  
  return x
```

- Created a dataframe to store results
```
df = pd.DataFrame(columns=['threads', 'time'])
def add_data(t, m):
    df.loc[len(df)] = [t, m]
    return df
```

- Calling the function and storing the results
```
for i in range(1,9):
    t=threadfn(i)
    add_data(i, int(t))
```

- plotting the results
![image](https://github.com/IkjotSingh221/MultiThreadingPython/assets/91063550/6b9d3492-c521-4950-b81a-c636fd0d6c8a)
