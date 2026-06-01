
library(qcc)
library(plotly)
library(htmlwidgets)

# Filter data for Machine 1, Pressure = 200kPa, Temp = 338K
data_m1 <- subset(X011, Machine == 1 & Pressure == 200 & Temperature == 338)

LSL = 45
USL = 55
TARGET = 50

# Create a qcc object for capability analysis
qcc_obj_m1_cap <- qcc(data_m1$PartLength, type="xbar.one", plot=FALSE)

# Process Capability Analysis
pc_m1 <- process.capability(qcc_obj_m1_cap, spec.limits=c(LSL, USL), target=TARGET, plot=FALSE)

# Plot the process capability chart
pc_m1_plot <- plot(pc_m1, title=paste0("Process Capability for Machine 1 (P=200kPa, T=338K)"))

# Placeholder for saving R code
