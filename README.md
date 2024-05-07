def findWaitingTime(processes, n, bt, wt, quantum):
    rem_bt = [0] * n
    # Copy the burst time into rt[]
    for i in range(n):
        rem_bt[i] = bt[i]
    t = 0  # Current time
    # Keep traversing processes in round
    # Robin manner until all of them aren't done.
    while 1:
        done = True
        # Traverse all processes one by
        # one repeatedly
        for i in range(n):

            # If burst time of a process is greater than 0 then only need to process further
            if rem_bt[i] > 0:
                done = False  # There is a pending process

                if rem_bt[i] > quantum:
                    # Increase the value of t i.e. shows
                    # how much time a process has been processed
                    t += quantum
                    # Decrease the burst_time of current
                    # process by quantum
                    rem_bt[i] -= quantum
                # If burst time is smaller than or equal
                # to quantum. Last cycle for this process
                else:
                    # Increase the value of t i.e. shows
                    # how much time a process has been processed
                    t = t + rem_bt[i]
                    # Waiting time is current time minus
                    # time used by this process
                    wt[i] = t - bt[i]
                    # As the process gets fully executed
                    # make its remaining burst time = 0
                    rem_bt[i] = 0

        if done:
            break


# Function to calculate turn around time
def findTurnAroundTime(processes, n, bt, wt, tat):
    # Calculating turnaround time
    for i in range(n):
        tat[i] = bt[i] + wt[i]
    # Function to calculate average waiting
    # and turn-around times.


def find_avgTime(processes, n, bt, quantum):
    wt = [0] * n
    tat = [0] * n

    # Function to find waiting time of all processes
    findWaitingTime(processes, n, bt,
                    wt, quantum)
    # Function to find turn around time for all processes
    findTurnAroundTime(processes, n, bt,
                       wt, tat)
    print("Processes Burst Time	 Waiting",
          "Time Turn-Around Time")
    total_wt = 0
    total_tat = 0
    for i in range(num):
        total_wt = total_wt + wt[i]
        total_tat = total_tat + tat[i]
        print(" ", i + 1, "\t\t", bt[i],
              "\t\t", wt[i], "\t\t", tat[i])

    print("\nAverage waiting time = %.5f " % (total_wt / num))
    print("Average turn around time = %.5f " % (total_tat / num))


# Driver code
if __name__ == "__main__":
    # Process id's
    proc = [i + 1 for i in range(40)]
    num = 40
    # Burst time of all processes (sample values)
    burst_time = [7, 5, 8, 9, 10, 6, 4, 8, 11, 7,
                  5, 8, 9, 10, 6, 4, 8, 11, 7, 5,
                  8, 9, 10, 6, 4, 8, 11, 7, 5, 8,
                  9, 10, 6, 4, 8, 11, 7, 5, 8, 9]

    quantum = 3
    find_avgTime(proc, num, burst_time, quantum)
