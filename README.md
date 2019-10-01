# ELK Stack

The Elastic Stack - that's Elasticsearch, Logstash, Kibana - are open
source projects that help you take data from any source, any format and search,
analyze, and visualize it in real time.

**Elasticsearch** is a distributed, open source search and analytics engine,
designed for horizontal scalability, reliability, and easy management. It
combines the speed of search with the power of analytics via a sophisticated,
developer-friendly query language covering structured, unstructured, and
time-series data.

**Logstash** is a flexible, open source data collection, enrichment, and
transportation pipeline. With connectors to common infrastructure for easy
integration, Logstash is designed to efficiently process a growing list of log,
event, and unstructured data sources for distribution into a variety of
outputs, including Elasticsearch.

**Kibana** is an open source data visualization platform that allows you to
interact with your data through stunning, powerful graphics. From histograms to
geomaps, Kibana brings your data to life with visuals that can be combined into
custom dashboards that help you share insights from your data far and wide.

This bundle is a 4 node cluster designed to scale out. Built around Elastic
components, it contains:

- 1 Logstash unit (minimum mem=3GB)
- 2 Elasticsearch units (minimum mem=7GB)
- 1 Kibana unit (minimum mem=3GB)

## Usage

    juju deploy ~elasticsearch-charmers/bundle/elk-stack

## Testing the deployment

The applications provide extended status reporting to indicate when they are
ready:

    juju status

This is particularly useful when combined with watch to track the on-going
progress of the deployment:

    watch juju status

The message for each unit will provide information about that unit's state.
Once they all indicate that they are ready, you can use the provided
`generate-noise` action to test that the Elastic Stack components are working
as expected:

    juju run-action logstash/0 generate-noise
    watch juju show-action-status

Once the action is complete, you can retrieve the results:

    juju show-action-output <action-id>

The &lt;action-id&gt; value will be in the `juju show-action-status`.

## Scale Out Usage

This bundle was designed to scale out. To increase the amount of log storage
and indexers, you can add-units to elasticsearch:

    juju add-unit elasticsearch

You can also increase in multiples. For example: increase the number of
logstash parser/shipping units with:

    juju add-unit -n 2 logstash


# Contact information

- Elasticsearch Charmers &lt;elasticsearch-charmers@lists.launchpad.net&gt;


# Need Help?

- [Juju mailing list](https://lists.ubuntu.com/mailman/listinfo/juju)
- [Juju Community](https://jujucharms.com/community)
