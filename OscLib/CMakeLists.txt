# optional stan dependency
if (STAN)
  set (STAN_TARGETS stan_math::stan_math SUNDIALS::kinsol_shared TBB::tbb)
endif (STAN)

add_library(OscLib
  SHARED
  EarthModel.cxx
  IOscCalc.cxx
  IOscCalcSterile.cxx
  OscCalc.cxx
  OscCalcAnalytic.cxx
  OscCalcCPT.cxx
  OscCalcDMP.cxx
  OscCalcDumb.cxx
  OscCalcGeneral.cxx
  OscCalcNuFast.cxx
  OscCalcPMNS_CPT.cxx
  OscCalcPMNS_NSI.cxx
  OscCalcPMNS.cxx
  OscCalcPMNSOpt.cxx
  OscCalcPMNSOptEigen.cxx
  OscCalcSterile.cxx
  OscCalcSterileBeam.cxx
  OscCalcSterileEigen.cxx
  PMNS_DMP.cxx
  PMNS_NSI.cxx
  PMNS_Sterile.cxx
  PMNS.cxx
  PMNSOpt.cxx
)

target_include_directories(OscLib PUBLIC
  $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/..>
  $<INSTALL_INTERFACE:include>
  )
target_link_libraries(OscLib PUBLIC ROOT::Core ROOT::Hist Eigen3::Eigen GSL::gsl Boost::boost ${STAN_TARGETS})
target_link_libraries(OscLib PRIVATE OscLib_Options)



