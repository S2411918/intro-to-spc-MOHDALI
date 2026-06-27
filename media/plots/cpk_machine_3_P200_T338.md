
library(qcc)

# Filter data for Machine 3, Pressure = 200kPa, Temp = 338K
data_m3 <- subset(X011, Machine == 3 & Pressure == 200 & Temperature == 338)

LSL = 45
USL = 55
TARGET = 50

# Create a qcc object for capability analysis
qcc_obj_m3_cap <- qcc(as.numeric(data_m3$PartLength), type="xbar.one", plot=FALSE)

# Process Capability Analysis
pc_m3 <- process.capability(qcc_obj_m3_cap, spec.limits=c(LSL, USL), target=TARGET)

# Extract Cpk value
cpk_m3 <- round(pc_m3$cpk, 4)

cat("Cpk for Machine 3 (P=200kPa, T=338K): ", cpk_m3)
