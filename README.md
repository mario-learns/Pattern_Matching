# Perf-Finder

# 1.0
# "Perfs" are what we use to measure the performance of individual cameras using GStreamer.
# We, the analysts, would get multiple lines of output that looked liked the following : GPU [1] PERF: [18663@0] 2.00  |  [18665@1] 2.00  |  [18667@2] 2.00  |  [18669@3] 2.00  |  [18671@4] # 2.00  |  [18673@5] 2.00  |  [18676@6] 2.00  |  [18678@7] 2.00  |  [18680@8] 2.00  |  [18682@9] 2.00  |  [18684@10] 1.00  |  [18686@11] 2.00  |  [18688@12] 2.00  |  [18690@13] 2.00  |  
# [18692@14] 2.00  |  [18694@15] 2.00  |  [18697@16] 2.00  |  [18700@17] 0.00  |  [18703@18] 0.00  |  [18706@19] 2.00  |  [18709@20] 2.00  |  [18712@21] 2.00  |  [18719@22] 2.00  |  [18722@23] 2.00  |  [18725@24] 2.00  |  [18729@25] 2.00  |  [18732@26] 2.00  |  [18735@27] 2.00  |  [18738@28] 1.67 
# A positive match would be indicated by @-.
# With no automation, the cyber analysts were becoming fatigued losing patience and motivation when there are about 100 line of entries to look at for the @- patterns to indicate a down camera.
# This initial script required setup and a ton of extra work. This was my starting point.
