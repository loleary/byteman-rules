# JBoss Operations Network
Various rule scripts and helpers used to debug, diagnose, support, and test various aspects of [Red Hat JBoss Operations Network](https://www.redhat.com/en/technologies/jboss-middleware/operations-network) and its upstream [RHQ Project](https://rhq-project.github.io/rhq/).

## JBM-BZ1594305
This is a JBoss ON server rule set that may be helpful in diagnosing 
ARJUNA012125 errors related to the exception `TransientPropertyValueException: object references an unsaved transient instance - save the transient instance before flushing: org.rhq.core.domain.measurement.MeasurementSchedule.baseline -> org.rhq.core.domain.measurement.MeasurementBaseline`

See [Red Hat Bugzilla 1594305](https://bugzilla.redhat.com/show_bug.cgi?id=1594305).

### To use this rule in a JBoss ON server:

1.  If necessary, download and install [JBoss Byteman](http://byteman.jboss.org/downloads).
2.  Set the envrionment variables `BYTEMAN_HOME`, `RHQ_SERVER_HOME`,
    and `BTM_PATH` to their appropriate values. 

        BYTEMAN_HOME=/usr/share/byteman
        RHQ_SERVER_HOME=/opt/jboss/on/jon-server
        BTM_PATH=/tmp/BZ1594305.btm

3.  Restart the JBoss ON server using the following command-line.

        RHQ_SERVER_ADDITIONAL_JAVA_OPTS="-javaagent:${BYTEMAN_HOME}/lib/byteman.jar=script:${BTM_PATH}" "${RHQ_SERVER_HOME}"/bin/rhqctl restart --server

