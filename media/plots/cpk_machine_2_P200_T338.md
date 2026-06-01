
library(qcc)

# Filter data for Machine 2, Pressure = 200kPa, Temp = 338K
data_m2 <- subset(X011, Machine == 2 & Pressure == 200 & Temperature == 338)

LSL = 45
USL = 55
TARGET = 50

# Create a qcc object for capability analysis
qcc_obj_m2_cap <- qcc(data_m2$PartLength, type="xbar.one", plot=FALSE)

# Process Capability Analysis
pc_m2 <- process.capability(qcc_obj_m2_cap, spec.limits=c(LSL, USL), target=TARGET, plot=FALSE)

# Extract Cpk value
cpk_m2 <- round(pc_m2$cpk, 4)

cat("Cpk for Machine 2 (P=200kPa, T=338K): ", cpk_m2)
